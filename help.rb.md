## Exmaples

```ruby
require 'obd'

obd = OBD.connect '/dev/tty.obd'

obd[:engine_rpm]
=> "4367.25rpm"

# Retrieve error codes
obd.send("03")
=> "43000545"
```


```ruby

start = Dir.glob("/dev/tty*")

# After connection
now = Dir.glob("/dev/tty*")
obd = Dir.glob("/dev/*obd*")

addt = now.reject{|x| start.include?(x)}
addt = nxt.reject{|x| now.include?(x)}
# This should give me the new device

```

```ruby
## Scratchpad

speed = obd.send("01 0D \r")
speed = obd.send("01 0D \r")
res = 
speed_hex = res.split(' ')
speed = float(int('0x'+speed_hex[3], 0 ))
```

- From sample.rb
```ruby
require 'obd'

obd = OBD.connect "/dev/tty.obd", 38400

loop do
  puts obd[:engine_rpm],
    obd[:vehicle_speed],
    obd.voltage,
    obd[:timing_advance]             + " - Timing Advance",
    obd[:engine_coolent_temperature] + " - Engine Coolant Temperature",
    obd[:calculated_engine_load]     + " - Calculated Engine Load",
    obd[:throttle_position]          + " - Throttle Position",
    obd[:aux_input_status]           + " - Aux input status",
    '-------------------------------'
end
```
---

## To output the /dev directory
`echo $(ls /dev/tty*) >> system.txt`

---
# From the help on `python-OBD`
https://github.com/brendan-w/python-OBD/issues/10

Thanks for bringing this up:

What little bluetooth information I have is actually from the upstream I forked from (which was linux). I don't have a mac, or the bluetooth module yet, but here are my thoughts so far:

- The library this uses for serial is called pySerial, so the problem is probably between that and your system.
- We need to positively identify which /dev port it's on. Other people that forked pyobd (the original library) say that it shows up on mac as /dev/tty.usbmodem*, or /dev/cu.*.
- If you've been using a USB bluetooth dongle, it might be worth trying to pair the adapter with the Mac itself.
- I'm not familiar with the Mac output, but you can try running dmesg right after plugging it in, to see what the system thinks it is. (You can also try doing a diff on ls /dev before and after connecting, to find out which port appears and disappears).
- In rare occurences under linux, my user didn't have permissions to let pySerial use the ports. A quick and dirty way to test this is to run python as root with sudo (a terrible solution, but could be informative)
- I fear that these suggestions may be no better than what you've already googled.
 
===
Thanks for the quick response! I now know for sure that /dev/tty.OBDII-Port is the port that I should be using. However, running python with sudo and enabling debug information didn't make any difference. I also tried running the following script:


``` ruby
# From the DevinBrown fork of OBD 
# PID file
{
    pids_supported_1: {
      mode: 0x01, pid: 0x00, size: 4, unit: "", description: "PIDs supported [01 - 20]",
      formula: -> (x) { 0 } #TODO
            },

    engine_rpm: {
      mode: 0x01, pid: 0x0C, size: 2, unit: :rpm, description: "Engine RPM",
      formula: -> (x) { ((256.0 * x[0]) + x[1]) / 4 }
            },
    vehicle_speed: {
      mode: 0x01, pid: 0x0D, size: 1, unit: :kmh, description: "Vehicle speed",
      formula: -> (x) { x[0] }
    }
}

def self.format_result command, result
      if result.nil? || result.empty?
        puts "Communication error: No data received. Check serial connection..."
        return ""
      end
      if is_command?(command) && result != "NO DATA"
        pid = pids[command.to_sym]
        pid[:formula].call convert_data(trim_data(result, pid[:size]))
      else
        result
      end
    end
