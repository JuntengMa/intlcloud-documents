## Overview

COS has integrated [Cloud Infinite](https://intl.cloud.tencent.com/document/product/1045) (CI), a one-stop professional multimedia solution that offers the image processing features outlined below. For more information, see [Image Processing Overview](https://intl.cloud.tencent.com/document/product/436/35280).

<table>
   <tr>
      <th>Service</td>
      <th>Feature</td>
      <th>Description</td>
   </tr>
   <tr>
      <td rowspan=12>Basic image processing service</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36366">Scaling</a></td>
      <td>Proportional scaling, scaling image to target width and height, and more</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36367">Cropping</a></td>
      <td>Cut (regular cropping), crop (scaling and cropping), iradius (inscribed circle cropping), and scrop (smart cropping)</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36368">Rotation</a></td>
      <td>Adaptive rotation and common rotation</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36369">Format conversion</a></td>
      <td>Format conversion, GIF optimization, and progressive display</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36370">Quality conversion</a></td>
      <td>Changes the quality of images in JPG and WEBP formats</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36371">Gaussian blur</a></td>
      <td>Blurs images</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36372">Sharpening</a></td>
      <td>Sharpens images</td>
   </tr>
   <tr>
      <td>Watermarking</td>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36373">Image watermarks</a>, <a href="https://intl.cloud.tencent.com/document/product/436/36374">text watermarks</a></td>
   </tr>
   <tr>
      <td>Obtaining image information</td>
      <td><a href="https://cloud.tencent.com/document/product/460/6927">Basic information</a>, <a href="https://cloud.tencent.com/document/product/460/6926">EXIF data</a>, <a href="https://cloud.tencent.com/document/product/460/6928">average hue</a></td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36378">Removing metadata</a></td>
      <td>Includes EXIF data</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/436/36379">Quick thumbnail template</a></td>
      <td>Performs quick format conversion, scaling, and cropping to generate thumbnails</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33443">Setting style</a></td>
      <td>Sets image styles to easily manage images for different purposes</td>
   </tr>
</table>


## SDK API Reference

For the parameters and method descriptions of all the APIs in the SDK, see [Api Documentation](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/).

## Using Image Processing when Uploading

The following example shows how COS automatically processes an image when you upload it.

Upon successful upload, COS will save both the original and processed images. You can obtain the processing result using a common download request.

#### Sample code

[//]: # ".cssg-snippet-upload-with-pic-operation"
```cs
PutObjectRequest request = new PutObjectRequest(bucket, key, srcPath);

JObject o = new JObject();
// Do not return the original image
o["is_pic_info"] = 0;
JArray rules = new JArray();
JObject rule = new JObject();
rule["bucket"] = bucket;
rule["fileid"] = key;
// Processing parameters. For the rules, see https://cloud.tencent.com/document/product/460/6924.
// This example proportionally scales the image to within 400 × 400 pixels
rule["rule"] = "imageView2/thumbnail/400x400";
rules.Add(rule);
o["rules"] = rules;

request.SetRequestHeader("Pic-Operation", o.ToString());
// Execute the request
PutObjectResult result = cosXml.PutObject(request);
```

>?For the complete sample, go to [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/dotnet/dist/PictureOperation.cs).
