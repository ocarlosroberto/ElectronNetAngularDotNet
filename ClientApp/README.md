# ElectronNetAngularDotNet

Angular SPA with dotnet core and Electron.NET

## How to create

First of all, create a new angular application with dotnet cli

```
dotnet new angular.
```

Next, include the Electorn.NET nuget package 

```
dotnet add package ElectronNET.API
```

Now, we need to change some code. First go to `Program.cs`

### Program.cs
```csharp
public static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureWebHostDefaults(webBuilder =>
        {
            webBuilder.UseElectron(args);
            webBuilder.UseStartup<Startup>();
        });
```

### Startup.cs
```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    ...

    // Open the Electron-Window here
    Task.Run(async () => await Electron.WindowManager.CreateWindowAsync());
}
```

## Start app

To start an ElectronNET app we need to install [`ElectronNET.CLI`](https://www.nuget.org/packages/ElectronNET.CLI/) as a global tool.

```
dotnet tool install ElectronNET.CLI -g
```

Now, in the first time, we need to run this command to initiaze our app:
```
electronize init
```

And to start our app we always run the command:
```
electronize start
```

## Publish app

To publish our app, we just need to run this command:
```
electronize build /target win
```

Your app setup will be deployed in `bin\Desktop` directory and the portable app will be in `bin\Desktop\win-unpacked`