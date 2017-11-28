Last login: Thu Oct  5 17:02:42 on ttys010
You have mail.

began@nycl97158m: ~/Box Sync/Discovery Family
$ pry
[1] pry(main)> now = Dir.glob("/dev/tty*")
=> ["/dev/tty",
 "/dev/ttyp0",
 "/dev/ttyp1",
 "/dev/ttyp2",
 "/dev/ttyp3",
 "/dev/ttyp4",
 "/dev/ttyp5",
 "/dev/ttyp6",
 "/dev/ttyp7",
 "/dev/ttyp8",
 "/dev/ttyp9",
 "/dev/ttypa",
 "/dev/ttypb",
 "/dev/ttypc",
 "/dev/ttypd",
 "/dev/ttype",
 "/dev/ttypf",
 "/dev/ttyq0",
 "/dev/ttyq1",
 "/dev/ttyq2",
 "/dev/ttyq3",
 "/dev/ttyq4",
 "/dev/ttyq5",
 "/dev/ttyq6",
 "/dev/ttyq7",
 "/dev/ttyq8",
 "/dev/ttyq9",
 "/dev/ttyqa",
 "/dev/ttyqb",
 "/dev/ttyqc",
 "/dev/ttyqd",
 "/dev/ttyqe",
 "/dev/ttyqf",
 "/dev/ttyr0",
 "/dev/ttyr1",
 "/dev/ttyr2",
 "/dev/ttyr3",
 "/dev/ttyr4",
 "/dev/ttyr5",
 "/dev/ttyr6",
 "/dev/ttyr7",
 "/dev/ttyr8",
[2] pry(main)> now.count
=> 141
[3] pry(main)> obd = Dir.glob("/dev/*obd*")
=> []
[4] pry(main)> now = Dir.glob("/dev/tty*")
=> ["/dev/tty",
 "/dev/ttyp0",
 "/dev/ttyp1",
 "/dev/ttyp2",
 "/dev/ttyp3",
 "/dev/ttyp4",
 "/dev/ttyp5",
 "/dev/ttyp6",
 "/dev/ttyp7",
 "/dev/ttyp8",
 "/dev/ttyp9",
 "/dev/ttypa",
 "/dev/ttypb",
 "/dev/ttypc",
 "/dev/ttypd",
 "/dev/ttype",
 "/dev/ttypf",
 "/dev/ttyq0",
 "/dev/ttyq1",
 "/dev/ttyq2",
 "/dev/ttyq3",
 "/dev/ttyq4",
 "/dev/ttyq5",
 "/dev/ttyq6",
 "/dev/ttyq7",
 "/dev/ttyq8",
 "/dev/ttyq9",
 "/dev/ttyqa",
 "/dev/ttyqb",
 "/dev/ttyqc",
 "/dev/ttyqd",
 "/dev/ttyqe",
 "/dev/ttyqf",
 "/dev/ttyr0",
 "/dev/ttyr1",
 "/dev/ttyr2",
 "/dev/ttyr3",
 "/dev/ttyr4",
 "/dev/ttyr5",
 "/dev/ttyr6",
 "/dev/ttyr7",
 "/dev/ttyr8",
[5] pry(main)> now.count
=> 141
[6] pry(main)> nxt = Dir.glob("/dev/tty*")
=> ["/dev/tty",
 "/dev/ttyp0",
 "/dev/ttyp1",
 "/dev/ttyp2",
 "/dev/ttyp3",
 "/dev/ttyp4",
 "/dev/ttyp5",
 "/dev/ttyp6",
 "/dev/ttyp7",
 "/dev/ttyp8",
 "/dev/ttyp9",
 "/dev/ttypa",
 "/dev/ttypb",
 "/dev/ttypc",
 "/dev/ttypd",
 "/dev/ttype",
 "/dev/ttypf",
 "/dev/ttyq0",
 "/dev/ttyq1",
 "/dev/ttyq2",
 "/dev/ttyq3",
 "/dev/ttyq4",
 "/dev/ttyq5",
 "/dev/ttyq6",
 "/dev/ttyq7",
 "/dev/ttyq8",
 "/dev/ttyq9",
 "/dev/ttyqa",
 "/dev/ttyqb",
 "/dev/ttyqc",
 "/dev/ttyqd",
 "/dev/ttyqe",
 "/dev/ttyqf",
 "/dev/ttyr0",
 "/dev/ttyr1",
 "/dev/ttyr2",
 "/dev/ttyr3",
 "/dev/ttyr4",
 "/dev/ttyr5",
 "/dev/ttyr6",
 "/dev/ttyr7",
 "/dev/ttyr8",
[7] pry(main)> nxt.count
=> 142
[8] pry(main)> addt = nxt.reject{|x| now.include?(x)}
=> ["/dev/tty.usbserial-A9CNJXDL"]
[9] pry(main)> require "obd"
=> true
[10] pry(main)> obd = OBD.connect addt[0]
=> #<OBD::Connection:0x007f9cb7822228 @baud=9600, @port="/dev/tty.usbserial-A9CNJXDL", @serial_port=#<SerialPort:fd 8>>
[11] pry(main)> obd[:engine_rpm]
=> "0.00rpm"
[12] pry(main)> obd.keys
NoMethodError: undefined method `keys' for #<OBD::Connection:0x007f9cb7822228>
from (pry):12:in `__pry__'
[13] pry(main)> obd.public_methods(false)
=> [:[], :send, :connect, :voltage]
[14] pry(main)> obd.voltage
=> "\xFC\x92\xFE\xFF"
[15] pry(main)> obd.send("03")
=> "\x9A\xFE"
[16] pry(main)> obd.send("02")
=> "\xFC\x92\xFE"
[17] pry(main)> obd.send("01 0D \r")
=> "\xFC\xFE\xFE\xFE\xFE\xFE"
[18] pry(main)> obd.send("01 0D")
=> "\xFE\xFE\xFE\xFE\xFF"
[19] pry(main)> speed = obd.send("01 0D")
=> "\xFC\xFE\xFE\xFE\xFE\xFF"
[20] pry(main)> speed = obd.send("01 0D")
=> "\xFE\xFE\xFE\xFE\xFF"
[21] pry(main)> speed_hex = speed.split(' ')
ArgumentError: invalid byte sequence in UTF-8
from (pry):21:in `split'
[22] pry(main)> speed_hex = speed.split('')
ArgumentError: invalid byte sequence in UTF-8
from (pry):22:in `split'
[23] pry(main)> speed_hex = speed.split(' ')
ArgumentError: invalid byte sequence in UTF-8
from (pry):23:in `split'
[24] pry(main)> speed_hex = speed.split("\\")
ArgumentError: invalid byte sequence in UTF-8
from (pry):24:in `split'
[25] pry(main)> speed_hex = speed.split("\\"))
SyntaxError: unexpected ')', expecting end-of-input
speed_hex = speed.split("\\"))
                              ^
[25] pry(main)> speed_hex = speed.split("\\\"))
[25] pry(main)*
[25] pry(main)* )
[25] pry(main)* "
[25] pry(main)* )
ArgumentError: invalid byte sequence in UTF-8
from (pry):25:in `split'
[26] pry(main)> speed_hex = speed.split("\"))
[26] pry(main)* "
[26] pry(main)* )
ArgumentError: invalid byte sequence in UTF-8
from (pry):30:in `split'
[27] pry(main)> speed_hex = speed.split("\\")
ArgumentError: invalid byte sequence in UTF-8
from (pry):33:in `split'
[28] pry(main)> speed.class
=> String
[29] pry(main)> class String
[29] pry(main)*   def convert_base(from, to)
[29] pry(main)*     self.to_i(from).to_s(to)
[29] pry(main)*     # works up-to base 36
[29] pry(main)*   end
[29] pry(main)* end
=> :convert_base
[30] pry(main)> speed_hex.convert_base(6,10)
NoMethodError: undefined method `convert_base' for nil:NilClass
from (pry):41:in `__pry__'
[31] pry(main)> speed.convert_base(6,10)
=> "0"
[32] pry(main)> obd[:fuel_pressure]
=> "0.00psi"
[33] pry(main)> obd[:vehicle_speed]
=> "0.00mph"
[34] pry(main)> fl = obd.send("2F 47")
=> "\xFC2\xFE\xBE\xBA\xFE"
[35] pry(main)> "%0.2f" % (fl * 100.0 / 255.0) + '%'
NoMethodError: undefined method `/' for #<String:0x007f9cb784ae58>
from (pry):46:in `__pry__'
[36] pry(main)> obd.pids
NoMethodError: undefined method `pids' for #<OBD::Connection:0x007f9cb7822228>
from (pry):47:in `__pry__'
[37] pry(main)> Obd.pids
NameError: uninitialized constant Obd
Did you mean?  OBD
from (pry):48:in `__pry__'
[38] pry(main)> OBD.pids
NoMethodError: undefined method `pids' for OBD:Module
from (pry):49:in `__pry__'
[39] pry(main)> fl.to_i(16)
=> 0
[40] pry(main)> v = obd[:voltage]
=> "\xFC\xF6\xFF\xFF\xFE\xFF"
[41] pry(main)> v.to_i(16)
=> 0
[42] pry(main)> v.to_f(16)
ArgumentError: wrong number of arguments (given 1, expected 0)
from (pry):53:in `to_f'
[43] pry(main)> v.to_f
=> 0.0
[44] pry(main)> l = lambda {|x,d| "%0.2f" % (d * 100.0 / 255.0) + '%'}
=> #<Proc:0x007f9cb88efb78@(pry):55 (lambda)>
[45] pry(main)> l.call(v, v.to_i(16))
=> "0.00%"
[46] pry(main)> l.call(fl, fl.to_i(16))
=> "0.00%"
[47] pry(main)> rp = lambda {|x,d| "%0.2f" % (d / 4.0) + 'rpm'}
=> #<Proc:0x007f9cb79aa8e8@(pry):58 (lambda)>
[48] pry(main)> rpm = obd[:rpm]
=> "\xFC\xF2\xFB\xFF"
[49] pry(main)> rp.call(rpm, rpm.to_i(16))
=> "0.00rpm"
[50] pry(main)> vin = obd.send("02 17")
=> "\xFC\x92\xFE\xFE\xBA\xFE"
[51] pry(main)> vin.to_i(16).to_s
=> "0"
[52] pry(main)> vin
=> "\xFC\x92\xFE\xFE\xBA\xFE"
[53] pry(main)> vin.hex
=> 0
[54] pry(main)> sp = obd.send("00 0")
=> "\xFC\xFE\xFE\xFE\xFE"
[55] pry(main)> sp.hex
=> 0
[56] pry(main)> sp.methods.grep(/hex/)
=> [:hex]
[57] pry(main)> sp.to_i(16).to_s(16)
=> "0"
[58] pry(main)> Integer(sp)
ArgumentError: invalid value for Integer(): "\xFC\xFE\xFE\xFE\xFE"
from (pry):69:in `Integer'
[59] pry(main)> sp.utf
NoMethodError: undefined method `utf' for "\xFC\xFE\xFE\xFE\xFE":String
from (pry):70:in `__pry__'
[60] pry(main)> sp.to_utf
NoMethodError: undefined method `to_utf' for "\xFC\xFE\xFE\xFE\xFE":String
Did you mean?  to_f
               to_str
from (pry):71:in `__pry__'
[61] pry(main)> sp.to_str
=> "\xFC\xFE\xFE\xFE\xFE"
[62] pry(main)> sp.to_str.split("F")
ArgumentError: invalid byte sequence in UTF-8
from (pry):73:in `split'
[63] pry(main)> sp.encoding
=> #<Encoding:UTF-8>
[64] pry(main)> sp.force_encoding('UTF-8')
=> "\xFC\xFE\xFE\xFE\xFE"
[65] pry(main)> s = sp.force_encoding('UTF-8')
=> "\xFC\xFE\xFE\xFE\xFE"
[66] pry(main)> s == sp
=> true
[67] pry(main)> sp.encode('UTF-8')
=> "\xFC\xFE\xFE\xFE\xFE"
[68] pry(main)> sp.encode('UTF-8').split("F")
ArgumentError: invalid byte sequence in UTF-8
from (pry):79:in `split'
[69] pry(main)> addt
=> ["/dev/tty.usbserial-A9CNJXDL"]
[70] pry(main)> obd.methods.grep(/con/)
=> [:connect]
[71] pry(main)> new_now = Dir.glob("/dev/tty*")
=> ["/dev/tty",
 "/dev/ttyp0",
 "/dev/ttyp1",
 "/dev/ttyp2",
 "/dev/ttyp3",
 "/dev/ttyp4",
 "/dev/ttyp5",
 "/dev/ttyp6",
 "/dev/ttyp7",
 "/dev/ttyp8",
 "/dev/ttyp9",
 "/dev/ttypa",
 "/dev/ttypb",
 "/dev/ttypc",
 "/dev/ttypd",
 "/dev/ttype",
 "/dev/ttypf",
 "/dev/ttyq0",
 "/dev/ttyq1",
 "/dev/ttyq2",
 "/dev/ttyq3",
 "/dev/ttyq4",
 "/dev/ttyq5",
 "/dev/ttyq6",
 "/dev/ttyq7",
 "/dev/ttyq8",
 "/dev/ttyq9",
 "/dev/ttyqa",
 "/dev/ttyqb",
 "/dev/ttyqc",
 "/dev/ttyqd",
 "/dev/ttyqe",
 "/dev/ttyqf",
 "/dev/ttyr0",
 "/dev/ttyr1",
 "/dev/ttyr2",
 "/dev/ttyr3",
 "/dev/ttyr4",
 "/dev/ttyr5",
 "/dev/ttyr6",
 "/dev/ttyr7",
 "/dev/ttyr8",
[72] pry(main)> new_now.count
=> 143
[73] pry(main)> ad = new_now.reject{|x| nxt.include?(x)}
=> ["/dev/ttys011"]
[74] pry(main)> ad
=> ["/dev/ttys011"]
[75] pry(main)> ad = new_now.reject{|x| now.include?(x)}
=> ["/dev/ttys011", "/dev/tty.usbserial-A9CNJXDL"]
[76] pry(main)> obd = OBD.connect ad.last
=> #<OBD::Connection:0x007f9cb78f9958 @baud=9600, @port="/dev/tty.usbserial-A9CNJXDL", @serial_port=#<SerialPort:fd 9>>
[77] pry(main)> obd.connecg
NoMethodError: undefined method `connecg' for #<OBD::Connection:0x007f9cb78f9958>
Did you mean?  connect
from (pry):88:in `__pry__'
[78] pry(main)> obd.connect
=> "\x9A\xFE\xFE\xFE"
[79] pry(main)> obd[:engine_rpm]
=> "0.00rpm"
[80] pry(main)> obd[:fuel_system_status]
ArgumentError: wrong number of arguments (given 2, expected 1)
from /Users/began/.rvm/gems/ruby-2.4.0@DISC/gems/obd-0.0.3/lib/obd/command.rb:40:in `block in pids'
[81] pry(main)> obd[:pids_supported_1]
=> [nil]
[82] pry(main)> obd[:intake_air_temperature]
=> "-104.00*F"
[83] pry(main)> obd[:throttle_position]
=> "0.00%"
[84] pry(main)> obd[:voltage]
=> "\xF6\xFF\xFF\xFE\xFF"
[85] pry(main)> obd.voltage
=> "\x92\xFE\xFF"
[86] pry(main)> obd.voltage.to_i(16).to_s(16)
=> "0"
[87] pry(main)> obd[:run_time_since_engine_start]
=> 0
[88] pry(main)> obd[:pids_supported_2]
=> [nil]
[89] pry(main)> obd[:engine_coolent_temperature]
=> "-104.00*F"
[90] pry(main)> addt
=> ["/dev/tty.usbserial-A9CNJXDL"]
[91] pry(main)>