# Nagios/icinga: check_timecapsule_public_ip

## Overview
Nagios/icinga check for monitoring public ip address of Apple Time Capsule. 

## Author

Copyright &copy; 2013, Markus Liljedahl <<markus@liljedahl.me>>

## Installation

In your Nagios plugins directory run

<pre><code>git clone git@github.com:mliljedahl/check_timecapsule_public_ip.git</code></pre>

### Requirements
Perl modules:

- SNMP
- Socket
- Nagios::Plugin

## Usage

### Install in Nagios/icinga

Edit your *commands.cfg* and add the following:

<pre><code>define command {
	command_name    check_timecapsule_public_ip
	command_line    $USER1$/check_timecapsule_public_ip -H $HOSTADDRESS$ -C '$ARG1$' -S '$ARG2$'
}</code></pre>

#### Monitor public ip
By default it uses the address defined for the *host* and for SNMP it uses *public* community version *2*.
<pre><code>define service{
	use						generic-service
	host_name				timecapsule
	service_description		Public IP
	check_command			check_timecapsule_public_ip
}</code></pre>

## Return codes
Code | Status   | Description
-----|----------|---------------------------
0    | OK       | No IP change, same IP address as before
1    | WARNING  | No old IP to compare with, can't determine if the IP address have changed or not
2    | CRITICAL | Public IP address have changed
3    | UNKNOWN  | Invalid command line arguments were supplied to the plugin or low-level failures

## License
check_timecapsule_public_ip is licensed under the [BSD License](https://github.com/mliljedahl/check_timecapsule_public_ip/blob/master/LICENSE).