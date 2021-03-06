Q42.HueApi
=========

Open source library for communication with the Philips Hue bridge.

This Portable Library is compatible with: .Net, Windows 8 and Windows Phone 8

Download directly from NuGet [Q42.HueApi on NuGet](https://nuget.org/packages/Q42.HueApi).

## How to use?
Some basic usage examples

### Bridge
Before you can communicate with the Philips Hue Bridge, you need to find the bridge and register your application:

	IBridgeLocator locator = new HttpBridgeLocator();
	
	//For Windows 8 and .NET45 projects you can use the SSDPBridgeLocator which actually scans your network. 
	//See the included BridgeDiscoveryTests and the specific .NET and .WinRT projects
    IEnumerable<string> bridgeIPs = await locator.LocateBridgesAsync(TimeSpan.FromSeconds(5));
	
Register your application
	
	HueClient client = new HueClient("ip");
	client.RegisterAsync("mypersonalappname", "mypersonalappkey");
	
If you already registered an appname, you can initialize the HueClient with the app's key:	

	client.Initialize("mypersonalappkey");

### Control the lights
Main usage of this library is to be able to control your lights. We use a LightCommand for that. A LightCommand can be send to one or more / multiple lights. A LightCommand can hold a color, effect, on/off etc.

	var command = new LightCommand();
	command.On = true;
	
There are some helpers to set a color on a command:
	
	//Turn the light on and set a Hex color for the command
	command.TurnOn().SetColor("FF00AA")
	
LightCommands also support Effects and Alerts

	//Blink once
	command.Alert = Alerts.Once;
	
	//Or start a colorloop
	command.Effect = Effects.ColorLoop;
	
Once you have composed your command, send it to one or more lights

	client.SendCommandAsync(command, new List<string> { "1" });
	
Or send it to all lights

	client.SendCommandAsync(command);

## How To install?
Download the source from GitHub or get the compiled assembly from NuGet [Q42.HueApi on NuGet](https://nuget.org/packages/Q42.HueApi).

## Credits
This library is made possible by contributions from:
* [Q42](http://www.q42.nl) ([@q42](http://twitter.com/q42))
* [@ermau](https://github.com/ermau/Q42.HueApi)

### Open Source Project Credits

* Newtonsoft.Json is used for object serialization

## License

Q42.HueApi is licensed under [MIT](http://www.opensource.org/licenses/mit-license.php "Read more about the MIT license form"). Refer to [license.txt](https://github.com/Q42/Q42.HueApi/blob/master/LICENSE.txt) for more information.

## Contributions

Contributions are welcome. Fork this repository and send a pull request if you have something useful to add.


## Related Projects
Other useful Philips Hue projects.

* [cDima Hue library](https://github.com/cDima/Hue) C# library
