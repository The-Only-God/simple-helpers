# simple-helpers

## Wallpapers

### Admin
```
Invoke-WebRequest -URI "https://github.com/The-Only-God/simple-helpers/blob/2828b0ecb0dbd05dbc3d0a03f1054df31b9c8b42/wallpaper-admin-danger.png?raw=true" -OutFile "wallpaper-admin-danger.png"
```


### User (Windows XP)
```
cd Downloads

Invoke-WebRequest -URI "https://github.com/The-Only-God/simple-helpers/blob/2828b0ecb0dbd05dbc3d0a03f1054df31b9c8b42/wallpaper-windows-xp.jpg?raw=true"  -OutFile "wallpaper-windows-xp.jpg"

$setwallpapersrc = @"
using System.Runtime.InteropServices;

public class Wallpaper
{
  public const int SetDesktopWallpaper = 20;
  public const int UpdateIniFile = 0x01;
  public const int SendWinIniChange = 0x02;
  [DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
  private static extern int SystemParametersInfo(int uAction, int uParam, string lpvParam, int fuWinIni);
  public static void SetWallpaper(string path)
  {
    SystemParametersInfo(SetDesktopWallpaper, 0, path, UpdateIniFile | SendWinIniChange);
  }
}
"@
Add-Type -TypeDefinition $setwallpapersrc

[Wallpaper]::SetWallpaper("$env:USERPROFILE\Downloads\wallpaper-windows-xp.jpg")
```
