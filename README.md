# Edi.UWP.Helpers
Helpers and Utils for Windows 10 UWP Projects. This document is not always keep updated with the library. Please check sample app also (also not always updated, what a big Ken it is!)

NuGet URL: [https://www.nuget.org/packages/Edi.UWP.Helpers/](https://www.nuget.org/packages/Edi.UWP.Helpers/)

Sample App: https://www.microsoft.com/zh-cn/store/apps/ediuwphelpers-sample-app/9wzdncrdxf3z

Author's Blog: [http://edi.wang](http://edi.wang)

---
V1.0.11

## Features

### Chinese Character Encoding

- big5.bin
- gb2312.bin
- DBCSEncoding.cs

#### Usage:

<pre>
using (var client = new HttpClient())
{
    client.BaseAddress = new Uri(ServiceEndpointUrl);
    var content = new FormUrlEncodedContent(new[] 
    {
        ...
    });
    var result = await client.PostAsync("", content);
    var resultContent = await result.Content.ReadAsByteArrayAsync();
    return DBCSEncoding.GetDBCSEncoding("gb2312").GetString(resultContent, 0,resultContent.Length - 1);
}
</pre>

### Windows Phone System Status Bar

internally reference: "Windows Mobile Extensions for the UWP"

namespace: Edi.UWP.Helpers.Mobile

##### Set Background and Foreground Color

<pre>
Edi.UWP.Helpers.Mobile.SetWindowsMobileStatusBarColor(Color.FromArgb(255, 0, 114, 188), Colors.White);
</pre>

#### Hide Status Bar

Hide System Status Bar on Phone, make App full screen

<pre>
Edi.UWP.Helpers.HideWindowsMobileStatusBar();
</pre>

##### Show Text and Progress on Status Bar

<pre>
Edi.UWP.Helpers.ShowSystemTrayAsync(Color backgroundColor, Color foregroundColor, double opacity = 1, string text = "", bool isIndeterminate = false, bool showProgress = false);
</pre>

### UI Helpers

##### Set App Window Launch Size

<pre>
Edi.UWP.Helpers.UI.SetWindowLaunchSize(720, 360);
</pre>

##### Set Color to App Title Bar

<pre>
void ApplyColorToTitleBar()
{
    Edi.UWP.Helpers.UI.ApplyColorToTitleBar(
        Color.FromArgb(255, 0, 114, 188), 
        Colors.White, 
        Colors.LightGray, 
        Colors.Gray);

    Edi.UWP.Helpers.UI.ApplyColorToTitleButton(
        Color.FromArgb(255, 0, 114, 188), Colors.White, 
        Color.FromArgb(255, 51, 148, 208), Colors.White,
        Color.FromArgb(255, 0, 114, 188), Colors.White, 
        Colors.LightGray, Colors.Gray);
}
</pre>

### Value Converters

Recommend to add the coverters to App.xaml in order to use them across all Xaml pages in your application

<pre>
&lt;Application
    ...
    xmlns:converters=&quot;using:Edi.UWP.Helpers.Converters&quot;&gt;
    &lt;Application.Resources&gt;
        ...
        &lt;converters:DateTimeToOffsetConverter x:Key=&quot;DateTimeToOffsetConverter&quot; /&gt;
        &lt;converters:StringFormatConverter x:Key=&quot;StringFormatConverter&quot; /&gt;
        &lt;converters:BooleanToVisibilityConverter x:Key=&quot;BooleanToVisibilityConverter&quot; /&gt;
        ...
    &lt;/Application.Resources&gt;
&lt;/Application&gt;
</pre>

// TODO
##### BitmapImageConverter
##### BooleanToVisibilityConverter
##### ColorHexStringToBrushConverter
##### ColorHexStringToColorConverter
##### ColorToCMYKStringConverter
##### ColorToHexStringConverter
##### ColorToRgbStringConverter
##### ColorToSolidColorBrushValueConverter
##### DateTimeToOffsetConverter
##### StringFormatConverters

<pre>
&lt;TextBlock Text=&quot;{Binding Date,Converter={StaticResource ResourceKey=StringFormat}, ConverterParameter=&#39;Last Update {0}&#39;}&quot; /&gt;
</pre>

### Windows 10 Tasks

// TODO

##### Redirect the user to Windows Store and open Review window for current App

<pre>
private async void BtnReview_OnClick(object sender, RoutedEventArgs e)
{
    await Edi.UWP.Helpers.Tasks.OpenStoreReviewAsync();
}
</pre>

##### Open Email Composing



### Selector Wrapper

// TODO

Edi.UWP.Helpers.WrapperBase&lt;T&gt;

Edi.UWP.Helpers.SelectorWrapper&lt;T&gt; : WrapperBase&lt;T&gt;, INotifyPropertyChanged

### Other Utility Functions

##### Copy string to ClipBoard

<pre>
Edi.UWP.Helpers.CopyToClipBoard("Hello");
</pre>

##### Check if device is connected to the Internet

<pre>
bool isConnected = Edi.UWP.Helpers.Utils.HasInternetConnection();
if (!isConnected)
{
    var dig = new MessageDialog("Please Check Internet Connection", "Are you TM kidding me?");
    await dig.ShowAsync();
    return;
}
</pre>

// TODO

##### Save InkCanvas strokes to .ink File

##### Load strokes from .ink file to InkCanvas

##### Convert ImageObject to Byte Array

##### Get Current App Version

<pre>
public string Version => Edi.UWP.Helpers.Utils.GetAppVersion();
</pre>

##### Get Current App Logo Image Uri

<pre>
public Uri Logo => Edi.UWP.Helpers.Utils.GetAppLogoUri();
...
&lt;Image Source=&quot;{Binding Logo}&quot; Stretch=&quot;None&quot; /&gt;
</pre>


##### Get Current App Display Name

<pre>
public string DisplayName => Edi.UWP.Helpers.Utils.GetAppDisplayName();
</pre>

##### Get Current App Publisher Name

<pre>
public string Publisher => Edi.UWP.Helpers.Utils.GetAppPublisher();
</pre>

### Extension Methods

// TODO

## License

The MIT License (MIT)
Copyright (c) 2016 edi.wang
Permission is hereby granted, free of charge, to any person obtaining a copyof this software and associated documentation files (the "Software"), to dealin the Software without restriction, including without limitation the rightsto use, copy, modify, merge, publish, distribute, sublicense, and/or sellcopies of the Software, and to permit persons to whom the Software isfurnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in allcopies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS ORIMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THEAUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHERLIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THESOFTWARE.