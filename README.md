# Take ScreenShot and Share to Whatsapp,Instagram,Gmail,...

# Let's Get Started
<H3>1 - Depend on it</h3>
<h6><b>Add it to your package's pubspec.yaml file</b></h6>
<pre>dependencies:
  screenshot: ^0.1.1
  esys_flutter_share: ^1.0.2</pre>
<H3>2 - Install it</h3>
<h6><b>Install packages from the command line</b></h6>
<pre>flutter packages get</pre>
<H3>2 - Getting Started</h3>
<h6><b>Import the package:</b></h6>
<pre>import 'dart:io';
import 'dart:typed_data';
import 'package:esys_flutter_share/esys_flutter_share.dart';
import 'package:flutter/material.dart';
import 'package:flutter/rendering.dart';
import 'package:screenshot/screenshot.dart';
import 'package:path_provider/path_provider.dart';</pre>

<h6><b>In buiild method wrap everything to Screenshot widget and pass instance of ScreenshotController to controller</b></h6>
<pre> ScreenshotController screenshotController = ScreenshotController();</pre>

<pre>@override
  Widget build(BuildContext context) {
    return Screenshot(
      controller: screenshotController,
      child: Scaffold(
        appBar: ....
        body: Container(
          ......// refer repository
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () async {
            _takeScreenshotandShare();
          },
          tooltip: 'Increment',
          child: Icon(Icons.share),
        ),
      ),
    );
  }</pre>
  
  <h6>Method for taking screenshot and sharing 
  
  <pre>_takeScreenshotandShare() async {
    _imageFile = null;
    screenshotController
        .capture(delay: Duration(milliseconds: 10), pixelRatio: 2.0)
        .then((File image) async {
      setState(() {
        _imageFile = image;
      });
      final directory = (await getApplicationDocumentsDirectory()).path;
      Uint8List pngBytes = _imageFile.readAsBytesSync();
      File imgFile = new File('$directory/screenshot.png');
      imgFile.writeAsBytes(pngBytes);
      print("File Saved to Gallery");
      await Share.file('Anupam', 'screenshot.png', pngBytes, 'image/png');
    }).catchError((onError) {
      print(onError);
    });
  }</pre>



## For referenece

![Alt Text](https://github.com/Anup2712/Sharescreenshot/blob/master/flow.gif)


