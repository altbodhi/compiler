after build cd to 
compiler\solution\CommandLine\bin\Release\net10.0
make Hello.znn  
```pascal
module Hello;
begin
  writeln("Hello, world!");
end Hello.
```

compiler and run:
```powershell
.\zc.exe /entry:Hello .\hello.znn  
dotnet exec --runtimeconfig .\zc.runtimeconfig.json .\hello.exe   
```
