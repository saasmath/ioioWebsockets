pyIOIOWebsockets

This is a collection of libraries and applications designed to provide access to an IOIO device via websocket connections - allowing not only access via standalone applications, but also from within a web browser itself[which is normally sandboxed and not allowed to access hardware devices such as serial ports, usb devices, or bluetooth connections]

Applications that run on the IOIO host provide a websocket connection[client or server] which is tied to the IOIO communication stream[typically the com port].

These applications can provide one of 2 protocols:
raw or websocket-ioio.   A raw protocol is just that, it takes whetever traffic it receives from the websocket and passes it to the ioio - if the data is invalid or corrupted this can lead to the IOIO being in a hung state waiting for the rest of a command that will never come.  The only way to recover is to reset the connection to the IOIO.

The websocket-ioio protocol will be a much more intelligent protocol, where the host application must check the command for validity and only send sane commands to the client.  By the same token it must provide feedback the sending application on if the command was invalid or valid, and when the command is executed.

Directory structure:
oneoffs: simple little apps created for learning and left for instructional notes
websocketApps: HTML5 websocket applications
websocketClients: daemons which bridge a host ioio device to a remote websocket server
websocketServers: daemons which bridge a host ioio device to a remote websocket client

Python applicationa use a number of add on modules:
  pyserial: http://pyserial.sourceforge.net/
  twisted
  autobahn python: http://autobahn.ws/python

Of specific note for developers is the pyserial module.  When installed, it will install a large number of sample programs which can be used with extremely little modification with the IOIO:
pyBusPirateLite and pyBusPirateLite1:  controls a buspirate microprocessor programmer via a serial connection.  This includes programatic access to i2c and spi - 2 protocols that the IOIO also allows access to.  Change the commands to match and you can write python applications to use i2c.
oscope_v1.2.py:

Attatches to some sort of microcontoller via the serial connection and starts reading the adc and charts the values.  Just needs a small ammount of changes in commands to accomodate the IOIO protocol.

