# ShellyLib-ERB NodeRed Flow
This is a ShellyLib Flow that reads Shelly Device CoAP Broadcast and outputs to status to Mqtt Broker. 
This also, can reads Mqtt Subsciptions to Set Shelly Switch Devices

# Some Detials:

Use at your own risk.
 
This is Demo/Example of a Node-Red Shelly-to-Mqtt Flow using 
factory Standard Firmware. Shelly Cloud must be turned ON.

It works very well for me, it does what I want.

This is "beta" release, updates may be coming.

# Goals and Implementation:

     1. Maintain use of Factory Firmware
     2. Continue Using the Shelly Cloud
     3. Support; Shelly-1, Shelly-2, and Shelly_HT
            (these are the only Shelly device types that I have access)
     4. Provide Shelly Device Status Reports to MQTT Broker
     5. Allow MQTT Topic Customization
     6. Allow for Custom MQTT Topic per Device via NickNames
     7. Allow single point of NickName Admin for Node-Red
            and MQTT Broker.
     8. Implement MQTT Last-WILL and Connection Status
     9. Retain all MQTT data
    10. Subscribe to MQTT Broker with "mqttPrefix" and then Decode and
            end "on/off" REST command to Shelly Switches.
    11. Allow use of: Shelly Device Names, NickNames, or IP Address
            for Shelly Switch Control
    12. Allow use or NOT of "/relay" within NickNames, and 
            MWTT Published commands.
    13. Provide User Option to Set MqttRetain flag

There maybe better methods to implement this flow,
    Contributors Welcome.
    
# Note:

    All examples and configurations; show my "mqttPrefix"
    which must be configured before use
    
# Note:

    This CoAP Shelly Decoder uses a "Brute Force" method
        of decoding, because; it is easy, simple,
        costomizable, and the Shelly CoAP packets are of
        known content.

# Note:

    The example nickNames the "User Perference" node are
        some that I use, they must be changed to be useful.

# To Use:

    Requirements: NodeRed Install "node-red-contrib-moment" via Manage Palett
    Note: This NodeRed Flow Tab must be "Enabled", it is provided "Disabled"
    Customize the "MQTT Pub" Node
        Set Mqtt Publish Broker Address and Port
        Set up Birth, Close, and Will Topics in Messages Tab
        Set Mqtt Broker Authentication as necessary
    Customize the "MQTT Sub SET" Node
        Set Mqtt Subscribe Node wiht Broker, Port, and Topic
        Set Mqtt Broker Authentication as necessary
    Customize "User Preferance" Node:
        Set up use.nickName to "true" or "false"
        Set up mqttRetain to "true" or "false"
        Set up NickNames
        Set up Mqtt topic Prefix
    Customize "ShellyTic" Node
        Set the desired Time Tic Interval
    Customize "Date/Format" Node
        Set Time Zone and Local Date Format
    The Debug and LOG outputs Nodes can be removed, 
        or just left turned off, as desired.
    
    
# Note:

    Shellys are very "chatty" on CoAP on the network
        as can be seen via the LOG output.

# Note:

    The ShellyLIb collects IPA from MQTT traffic of Shelly Device for later
        use as Aliases and REST Commands.
        
# Example MQTT Pub Commands (each group does the samething):

    On/Off is NOT case sensitive, topic is case sensitive
    -
    mosquitto_pub -t ebconpri/shelly/SHSW-1/32C849/relay/0/Set -m off
    mosquitto_pub -t ebconpri/shelly/SHSW-1/32C849/0/Set -m ofF
    mosquitto_pub -t ebconpri/shelly/Hab/Fan/0/set -m off
    mosquitto_pub -t ebconpri/shelly/192.168.0.220/0/set -m off
    mosquitto_pub -t ebconpri/shelly/192.168.0.220/0/set -m off
    -
    mosquitto_pub -t ebconpri/shelly/Hab/Sink/0/set -m on
    mosquitto_pub -t ebconpri/shelly/Hab/Sink/relay/0/set -m On
    
    
# Example Mqtt Broker Subscribe Output:

    ebconpri/shelly/ShellyLib/Rev ERB-0.24.D
    ebconpri/shelly/ShellyLib/Tic 1547852624 2019/01/18 15:03:44 -0800
    ebconpri/shelly/Lab/WB-3D/0 on
    ebconpri/shelly/SHSW-1/12C4EB/0/ip 192.168.0.225
    ebconpri/shelly/Lab/WB-3D/0/ip 192.168.0.225
    ebconpri/shelly/Hab/Bed-Light/0 off
    ebconpri/shelly/Lab/Displays/0 on
    ebconpri/shelly/Lab/Work-Light/0 on
    ebconpri/shelly/Lab/Bench-Power/0 on
    ebconpri/shelly/ShellyLib/Tic 1547852834 2019/01/18 15:07:14 -0800
    ebconpri/shelly/Temp/Shop/C 9.0
    ebconpri/shelly/Temp/Shop/F 48.2
    ebconpri/shelly/Temp/Shop/H 70.0
    ebconpri/shelly/ShellyLib/Tic 1547852854 2019/01/18 15:07:34 -0800
    ebconpri/shelly/Temp/Lab/C 23.6
    ebconpri/shelly/Temp/Lab/F 74.5
    -
    ebconpri/shelly/Hab/Sink/0/set on
    ebconpri/shelly/192.168.0.220/0/set OFF


# TBD:

    Add a NodeRed Dashboard for Shelly Devices
    Represent Shelly-2 Power Better.
    List Discoverd Devices as New.
    Remove 404 Chat back from Node-Red UDP/CoAP.
    Maybe add JSON output.


# History:

    Rev: ERB-0.next
        Clean Up
        Now Requires Moment Node to be Installed
        Added Human Readable Time Tic
        Suggests Customized Tic: Date, Time Format and Interval
        Set all Mqtt Data to Retain
        Added MQTT Subscribe to "mqttPrefix" to send 
            REST "on/off" command to Shelly
    Rev: ERB-0.20 - Initial Release
    
# End
