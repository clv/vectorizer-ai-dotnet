# Vectorizer.AI.Api.VectorizationApi

All URIs are relative to *https://api.vectorizer.ai/api/v1*

| Method | HTTP request | Description |
|--------|--------------|-------------|
| [**PostDelete**](VectorizationApi.md#postdelete) | **POST** /delete | Delete a retained image |
| [**PostDownload**](VectorizationApi.md#postdownload) | **POST** /download | Download a retained result |
| [**PostVectorize**](VectorizationApi.md#postvectorize) | **POST** /vectorize | Vectorize an image |

<a id="postdelete"></a>
# **PostDelete**
> DeleteImageResponse PostDelete (string imageToken)

Delete a retained image

Delete a retained image and result before its retention period expires.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Vectorizer.AI.Api;
using Vectorizer.AI.Client;
using Vectorizer.AI.Model;

namespace Example
{
    public class PostDeleteExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.vectorizer.ai/api/v1";
            // Configure HTTP basic authorization: basicAuth
            config.Username = "YOUR_USERNAME";
            config.Password = "YOUR_PASSWORD";

            var apiInstance = new VectorizationApi(config);
            var imageToken = "imageToken_example";  // string | Image Token to delete before its retention period expires.

            try
            {
                // Delete a retained image
                DeleteImageResponse result = apiInstance.PostDelete(imageToken);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling VectorizationApi.PostDelete: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the PostDeleteWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Delete a retained image
    ApiResponse<DeleteImageResponse> response = apiInstance.PostDeleteWithHttpInfo(imageToken);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling VectorizationApi.PostDeleteWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **imageToken** | **string** | Image Token to delete before its retention period expires. |  |

### Return type

[**DeleteImageResponse**](DeleteImageResponse.md)

### Authorization

[basicAuth](../README.md#basicAuth)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The Image Token was deleted. |  -  |
| **400** | Invalid request parameters, image input, URL fetch, or Image Token. |  -  |
| **401** | Missing or invalid API credentials. |  * WWW-Authenticate - HTTP Basic authentication challenge returned with 401 responses. <br>  |
| **402** | The account does not have an API subscription, is past due, or is out of credits. |  -  |
| **413** | The uploaded image, fetched image, or requested PNG output is too large. |  -  |
| **429** | Rate limit exceeded. Back off before retrying. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |
| **500** | Unexpected internal error. |  -  |
| **503** | Temporary overload or internal processing timeout. Retry later. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="postdownload"></a>
# **PostDownload**
> System.IO.Stream PostDownload (string imageToken, string receipt = null, string outputFileFormat = null, string outputShapeStacking = null, string outputGroupBy = null, string outputDrawStyle = null, float? outputStrokesStrokeWidth = null, bool? outputStrokesNonScalingStroke = null, bool? outputStrokesUseOverrideColor = null, string outputStrokesOverrideColor = null, bool? outputGapFillerEnabled = null, bool? outputGapFillerNonScalingStroke = null, bool? outputGapFillerClip = null, float? outputGapFillerStrokeWidth = null, bool? outputParameterizedShapesFlatten = null, float? outputCurvesLineFitTolerance = null, bool? outputCurvesAllowedQuadraticBezier = null, bool? outputCurvesAllowedCubicBezier = null, bool? outputCurvesAllowedCircularArc = null, bool? outputCurvesAllowedEllipticalArc = null, string outputSvgVersion = null, bool? outputSvgFixedSize = null, bool? outputSvgAdobeCompatibilityMode = null, string outputPdfVersion = null, string outputPdfCompressionMode = null, string outputEpsVersion = null, string outputDxfCompatibilityLevel = null, string outputBitmapAntiAliasingMode = null, float? outputSizeScale = null, float? outputSizeWidth = null, float? outputSizeHeight = null, string outputSizeUnit = null, string outputSizeAspectRatio = null, float? outputSizeAlignX = null, float? outputSizeAlignY = null, float? outputSizeInputDpi = null, float? outputSizeOutputDpi = null)

Download a retained result

Download a production result from a retained Image Token, optionally changing output.file_format and other output options. Include receipt when downloading additional formats after upgrading a preview result.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Vectorizer.AI.Api;
using Vectorizer.AI.Client;
using Vectorizer.AI.Model;

namespace Example
{
    public class PostDownloadExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.vectorizer.ai/api/v1";
            // Configure HTTP basic authorization: basicAuth
            config.Username = "YOUR_USERNAME";
            config.Password = "YOUR_PASSWORD";

            var apiInstance = new VectorizationApi(config);
            var imageToken = "imageToken_example";  // string | Image Token returned from a vectorize request with policy.retention_days > 0.
            var receipt = "receipt_example";  // string | Receipt returned in the X-Receipt response header when upgrading a preview result to production. Include it when downloading additional formats from that upgraded preview. (optional) 
            var outputFileFormat = "svg";  // string | Output file format to generate. (optional)  (default to svg)
            var outputShapeStacking = "cutouts";  // string | Whether shapes are cut out of each other or stacked atop each other. (optional)  (default to cutouts)
            var outputGroupBy = "none";  // string | Grouping of shapes in output. (optional)  (default to none)
            var outputDrawStyle = "fill_shapes";  // string | How shapes are rendered. (optional)  (default to fill_shapes)
            var outputStrokesStrokeWidth = 1F;  // float? | Width of stroke for shape outlines (when enabled). (optional)  (default to 1F)
            var outputStrokesNonScalingStroke = true;  // bool? | Use non-scaling strokes when drawing shape outlines. (optional)  (default to true)
            var outputStrokesUseOverrideColor = false;  // bool? | Override shape color with a specific color. (optional)  (default to false)
            var outputStrokesOverrideColor = "\"#000000\"";  // string | Color value to override shape stroke color if enabled. Must be in '#RRGGBB' or 'rgba(r,g,b,a)' format. (optional)  (default to "#000000")
            var outputGapFillerEnabled = true;  // bool? | Enable filling small visual gaps caused by vector rendering artifacts. (optional)  (default to true)
            var outputGapFillerNonScalingStroke = true;  // bool? | Use non-scaling strokes for gap filling. (optional)  (default to true)
            var outputGapFillerClip = false;  // bool? | Clip gap filler strokes to shape bounds when stacking shapes. (optional)  (default to false)
            var outputGapFillerStrokeWidth = 2F;  // float? | Width of the gap filler strokes (in output units). (optional)  (default to 2F)
            var outputParameterizedShapesFlatten = false;  // bool? | Whether to flatten detected circles, rectangles, and stars to curves. (optional)  (default to false)
            var outputCurvesLineFitTolerance = 0.1F;  // float? | Maximum allowed error when approximating curves with line segments. (optional)  (default to 0.1F)
            var outputCurvesAllowedQuadraticBezier = true;  // bool? | Allow quadratic Bézier curves in the output. (optional)  (default to true)
            var outputCurvesAllowedCubicBezier = true;  // bool? | Allow cubic Bézier curves in the output. (optional)  (default to true)
            var outputCurvesAllowedCircularArc = true;  // bool? | Allow circular arcs in the output. (optional)  (default to true)
            var outputCurvesAllowedEllipticalArc = true;  // bool? | Allow elliptical arcs in the output. (optional)  (default to true)
            var outputSvgVersion = "svg_1_0";  // string | SVG version to declare in the SVG output. (optional)  (default to svg_1_1)
            var outputSvgFixedSize = false;  // bool? | Whether to fix the SVG dimensions in the output file. (optional)  (default to false)
            var outputSvgAdobeCompatibilityMode = false;  // bool? | Enable Illustrator compatibility by disabling unsupported SVG features. (optional)  (default to false)
            var outputPdfVersion = "PDF_1_4";  // string | PDF version to generate for PDF output. (optional)  (default to PDF_1_4)
            var outputPdfCompressionMode = "None";  // string | Compression method to apply to PDF output streams. (optional)  (default to Deflate)
            var outputEpsVersion = "PS_3_0_EPSF_3_0";  // string | EPS format version for EPS output. (optional)  (default to PS_3_0_EPSF_3_0)
            var outputDxfCompatibilityLevel = "lines_only";  // string | Level of primitive support for DXF output. (optional)  (default to lines_and_arcs)
            var outputBitmapAntiAliasingMode = "anti_aliased";  // string | Anti-aliasing mode for bitmap (PNG) output. (optional)  (default to anti_aliased)
            var outputSizeScale = 3.4F;  // float? | Overall uniform scaling factor for the output image. (optional) 
            var outputSizeWidth = 3.4F;  // float? | Output width, in the selected unit (see output.size.unit). (optional) 
            var outputSizeHeight = 3.4F;  // float? | Output height, in the selected unit (see output.size.unit). (optional) 
            var outputSizeUnit = "none";  // string | Measurement unit for output dimensions. (optional)  (default to none)
            var outputSizeAspectRatio = "preserve_inset";  // string | How to preserve or stretch aspect ratio. (optional)  (default to preserve_inset)
            var outputSizeAlignX = 0.5F;  // float? | Horizontal alignment (0.0 = left, 0.5 = center, 1.0 = right) when aspect ratio is preserved. (optional)  (default to 0.5F)
            var outputSizeAlignY = 0.5F;  // float? | Vertical alignment (0.0 = top, 0.5 = center, 1.0 = bottom) when aspect ratio is preserved. (optional)  (default to 0.5F)
            var outputSizeInputDpi = 3.4F;  // float? | Override the detected DPI of the input image for size computations. (optional) 
            var outputSizeOutputDpi = 3.4F;  // float? | DPI setting for the output image. (optional) 

            try
            {
                // Download a retained result
                System.IO.Stream result = apiInstance.PostDownload(imageToken, receipt, outputFileFormat, outputShapeStacking, outputGroupBy, outputDrawStyle, outputStrokesStrokeWidth, outputStrokesNonScalingStroke, outputStrokesUseOverrideColor, outputStrokesOverrideColor, outputGapFillerEnabled, outputGapFillerNonScalingStroke, outputGapFillerClip, outputGapFillerStrokeWidth, outputParameterizedShapesFlatten, outputCurvesLineFitTolerance, outputCurvesAllowedQuadraticBezier, outputCurvesAllowedCubicBezier, outputCurvesAllowedCircularArc, outputCurvesAllowedEllipticalArc, outputSvgVersion, outputSvgFixedSize, outputSvgAdobeCompatibilityMode, outputPdfVersion, outputPdfCompressionMode, outputEpsVersion, outputDxfCompatibilityLevel, outputBitmapAntiAliasingMode, outputSizeScale, outputSizeWidth, outputSizeHeight, outputSizeUnit, outputSizeAspectRatio, outputSizeAlignX, outputSizeAlignY, outputSizeInputDpi, outputSizeOutputDpi);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling VectorizationApi.PostDownload: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the PostDownloadWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Download a retained result
    ApiResponse<System.IO.Stream> response = apiInstance.PostDownloadWithHttpInfo(imageToken, receipt, outputFileFormat, outputShapeStacking, outputGroupBy, outputDrawStyle, outputStrokesStrokeWidth, outputStrokesNonScalingStroke, outputStrokesUseOverrideColor, outputStrokesOverrideColor, outputGapFillerEnabled, outputGapFillerNonScalingStroke, outputGapFillerClip, outputGapFillerStrokeWidth, outputParameterizedShapesFlatten, outputCurvesLineFitTolerance, outputCurvesAllowedQuadraticBezier, outputCurvesAllowedCubicBezier, outputCurvesAllowedCircularArc, outputCurvesAllowedEllipticalArc, outputSvgVersion, outputSvgFixedSize, outputSvgAdobeCompatibilityMode, outputPdfVersion, outputPdfCompressionMode, outputEpsVersion, outputDxfCompatibilityLevel, outputBitmapAntiAliasingMode, outputSizeScale, outputSizeWidth, outputSizeHeight, outputSizeUnit, outputSizeAspectRatio, outputSizeAlignX, outputSizeAlignY, outputSizeInputDpi, outputSizeOutputDpi);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling VectorizationApi.PostDownloadWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **imageToken** | **string** | Image Token returned from a vectorize request with policy.retention_days &gt; 0. |  |
| **receipt** | **string** | Receipt returned in the X-Receipt response header when upgrading a preview result to production. Include it when downloading additional formats from that upgraded preview. | [optional]  |
| **outputFileFormat** | **string** | Output file format to generate. | [optional] [default to svg] |
| **outputShapeStacking** | **string** | Whether shapes are cut out of each other or stacked atop each other. | [optional] [default to cutouts] |
| **outputGroupBy** | **string** | Grouping of shapes in output. | [optional] [default to none] |
| **outputDrawStyle** | **string** | How shapes are rendered. | [optional] [default to fill_shapes] |
| **outputStrokesStrokeWidth** | **float?** | Width of stroke for shape outlines (when enabled). | [optional] [default to 1F] |
| **outputStrokesNonScalingStroke** | **bool?** | Use non-scaling strokes when drawing shape outlines. | [optional] [default to true] |
| **outputStrokesUseOverrideColor** | **bool?** | Override shape color with a specific color. | [optional] [default to false] |
| **outputStrokesOverrideColor** | **string** | Color value to override shape stroke color if enabled. Must be in &#39;#RRGGBB&#39; or &#39;rgba(r,g,b,a)&#39; format. | [optional] [default to &quot;#000000&quot;] |
| **outputGapFillerEnabled** | **bool?** | Enable filling small visual gaps caused by vector rendering artifacts. | [optional] [default to true] |
| **outputGapFillerNonScalingStroke** | **bool?** | Use non-scaling strokes for gap filling. | [optional] [default to true] |
| **outputGapFillerClip** | **bool?** | Clip gap filler strokes to shape bounds when stacking shapes. | [optional] [default to false] |
| **outputGapFillerStrokeWidth** | **float?** | Width of the gap filler strokes (in output units). | [optional] [default to 2F] |
| **outputParameterizedShapesFlatten** | **bool?** | Whether to flatten detected circles, rectangles, and stars to curves. | [optional] [default to false] |
| **outputCurvesLineFitTolerance** | **float?** | Maximum allowed error when approximating curves with line segments. | [optional] [default to 0.1F] |
| **outputCurvesAllowedQuadraticBezier** | **bool?** | Allow quadratic Bézier curves in the output. | [optional] [default to true] |
| **outputCurvesAllowedCubicBezier** | **bool?** | Allow cubic Bézier curves in the output. | [optional] [default to true] |
| **outputCurvesAllowedCircularArc** | **bool?** | Allow circular arcs in the output. | [optional] [default to true] |
| **outputCurvesAllowedEllipticalArc** | **bool?** | Allow elliptical arcs in the output. | [optional] [default to true] |
| **outputSvgVersion** | **string** | SVG version to declare in the SVG output. | [optional] [default to svg_1_1] |
| **outputSvgFixedSize** | **bool?** | Whether to fix the SVG dimensions in the output file. | [optional] [default to false] |
| **outputSvgAdobeCompatibilityMode** | **bool?** | Enable Illustrator compatibility by disabling unsupported SVG features. | [optional] [default to false] |
| **outputPdfVersion** | **string** | PDF version to generate for PDF output. | [optional] [default to PDF_1_4] |
| **outputPdfCompressionMode** | **string** | Compression method to apply to PDF output streams. | [optional] [default to Deflate] |
| **outputEpsVersion** | **string** | EPS format version for EPS output. | [optional] [default to PS_3_0_EPSF_3_0] |
| **outputDxfCompatibilityLevel** | **string** | Level of primitive support for DXF output. | [optional] [default to lines_and_arcs] |
| **outputBitmapAntiAliasingMode** | **string** | Anti-aliasing mode for bitmap (PNG) output. | [optional] [default to anti_aliased] |
| **outputSizeScale** | **float?** | Overall uniform scaling factor for the output image. | [optional]  |
| **outputSizeWidth** | **float?** | Output width, in the selected unit (see output.size.unit). | [optional]  |
| **outputSizeHeight** | **float?** | Output height, in the selected unit (see output.size.unit). | [optional]  |
| **outputSizeUnit** | **string** | Measurement unit for output dimensions. | [optional] [default to none] |
| **outputSizeAspectRatio** | **string** | How to preserve or stretch aspect ratio. | [optional] [default to preserve_inset] |
| **outputSizeAlignX** | **float?** | Horizontal alignment (0.0 &#x3D; left, 0.5 &#x3D; center, 1.0 &#x3D; right) when aspect ratio is preserved. | [optional] [default to 0.5F] |
| **outputSizeAlignY** | **float?** | Vertical alignment (0.0 &#x3D; top, 0.5 &#x3D; center, 1.0 &#x3D; bottom) when aspect ratio is preserved. | [optional] [default to 0.5F] |
| **outputSizeInputDpi** | **float?** | Override the detected DPI of the input image for size computations. | [optional]  |
| **outputSizeOutputDpi** | **float?** | DPI setting for the output image. | [optional]  |

### Return type

**System.IO.Stream**

### Authorization

[basicAuth](../README.md#basicAuth)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: image/svg+xml, application/postscript, application/pdf, application/dxf, image/png, application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The requested output file. |  * Content-Disposition - Suggested filename for the generated result. <br>  * Content-Encoding - May be gzip for SVG, EPS, or DXF responses when the request allows gzip encoding. <br>  * X-Receipt - Returned when a preview Image Token is upgraded to a production result; use it for discounted additional format downloads. <br>  * X-Credits-Charged - Credits charged for the request. This is 0 for test requests. <br>  * X-Credits-Calculated - Returned for test requests to show the credits that would have been charged for the equivalent non-test request. <br>  |
| **400** | Invalid request parameters, image input, URL fetch, or Image Token. |  -  |
| **401** | Missing or invalid API credentials. |  * WWW-Authenticate - HTTP Basic authentication challenge returned with 401 responses. <br>  |
| **402** | The account does not have an API subscription, is past due, or is out of credits. |  -  |
| **413** | The uploaded image, fetched image, or requested PNG output is too large. |  -  |
| **429** | Rate limit exceeded. Back off before retrying. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |
| **500** | Unexpected internal error. |  -  |
| **503** | Temporary overload or internal processing timeout. Retry later. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

<a id="postvectorize"></a>
# **PostVectorize**
> System.IO.Stream PostVectorize (System.IO.Stream image = null, string imageUrl = null, byte[] imageBase64 = null, string imageToken = null, string mode = null, int? inputMaxPixels = null, int? policyRetentionDays = null, int? processingMaxColors = null, float? processingShapesMinAreaPx = null, string processingPalette = null, string processingColorProfileInput = null, string processingColorProfileOutput = null, bool? processingParameterizedShapesEllipseGeneralEnabled = null, bool? processingParameterizedShapesEllipseCircleEnabled = null, bool? processingParameterizedShapesTriangleGeneralEnabled = null, bool? processingParameterizedShapesTriangleIsoscelesEnabled = null, bool? processingParameterizedShapesQuadrilateralGeneralEnabled = null, bool? processingParameterizedShapesQuadrilateralRectangleEnabled = null, bool? processingParameterizedShapesQuadrilateralBulletEnabled = null, bool? processingParameterizedShapesStarN3Enabled = null, bool? processingParameterizedShapesStarN4Enabled = null, bool? processingParameterizedShapesStarN5Enabled = null, bool? processingParameterizedShapesStarN6Enabled = null, string outputFileFormat = null, string outputShapeStacking = null, string outputGroupBy = null, string outputDrawStyle = null, float? outputStrokesStrokeWidth = null, bool? outputStrokesNonScalingStroke = null, bool? outputStrokesUseOverrideColor = null, string outputStrokesOverrideColor = null, bool? outputGapFillerEnabled = null, bool? outputGapFillerNonScalingStroke = null, bool? outputGapFillerClip = null, float? outputGapFillerStrokeWidth = null, bool? outputParameterizedShapesFlatten = null, float? outputCurvesLineFitTolerance = null, bool? outputCurvesAllowedQuadraticBezier = null, bool? outputCurvesAllowedCubicBezier = null, bool? outputCurvesAllowedCircularArc = null, bool? outputCurvesAllowedEllipticalArc = null, string outputSvgVersion = null, bool? outputSvgFixedSize = null, bool? outputSvgAdobeCompatibilityMode = null, string outputPdfVersion = null, string outputPdfCompressionMode = null, string outputEpsVersion = null, string outputDxfCompatibilityLevel = null, string outputBitmapAntiAliasingMode = null, float? outputSizeScale = null, float? outputSizeWidth = null, float? outputSizeHeight = null, string outputSizeUnit = null, string outputSizeAspectRatio = null, float? outputSizeAlignX = null, float? outputSizeAlignY = null, float? outputSizeInputDpi = null, float? outputSizeOutputDpi = null)

Vectorize an image

Submit exactly one image source as multipart form data: image, image.url, image.base64, or image.token. The response body is the generated SVG, EPS, PDF, DXF, or PNG file selected by output.file_format. Clients should allow an idle timeout of at least 180 seconds.

### Example
```csharp
using System.Collections.Generic;
using System.Diagnostics;
using Vectorizer.AI.Api;
using Vectorizer.AI.Client;
using Vectorizer.AI.Model;

namespace Example
{
    public class PostVectorizeExample
    {
        public static void Main()
        {
            Configuration config = new Configuration();
            config.BasePath = "https://api.vectorizer.ai/api/v1";
            // Configure HTTP basic authorization: basicAuth
            config.Username = "YOUR_USERNAME";
            config.Password = "YOUR_PASSWORD";

            var apiInstance = new VectorizationApi(config);
            var image = new System.IO.MemoryStream(System.IO.File.ReadAllBytes("/path/to/file.txt"));  // System.IO.Stream | Binary file upload of the image to vectorize. Accepts .bmp, .gif, .jpeg, .png, or .tiff files. (optional) 
            var imageUrl = "imageUrl_example";  // string | URL to fetch the input image from for vectorization. (optional) 
            var imageBase64 = System.Text.Encoding.ASCII.GetBytes("BYTE_ARRAY_DATA_HERE");  // byte[] | Base64-encoded string of the input image. Maximum size 1 megabyte. (optional) 
            var imageToken = "imageToken_example";  // string | An Image Token returned from an earlier vectorization call with policy.retention_days > 0. (optional) 
            var mode = "production";  // string | Mode of operation, useful during integration work. (optional)  (default to production)
            var inputMaxPixels = 2097252;  // int? | Maximum input image size (width × height in pixels) before resizing. (optional)  (default to 2097252)
            var policyRetentionDays = 0;  // int? | Number of days to retain the uploaded image and its results for re-use. (optional)  (default to 0)
            var processingMaxColors = 0;  // int? | Maximum number of colors allowed in the vectorization result. 0 means unlimited. (optional)  (default to 0)
            var processingShapesMinAreaPx = 0.125F;  // float? | Minimum shape area (in pixels) to keep in the result; smaller shapes are discarded. (optional)  (default to 0.125F)
            var processingPalette = "processingPalette_example";  // string | Palette remapping and color control, using '[color][-> remapped][~ tolerance];' format. (optional) 
            var processingColorProfileInput = "ignore";  // string | How to handle ICC profiles embedded in input images. (optional)  (default to ignore)
            var processingColorProfileOutput = "\"ignore\"";  // string | ICC profile behavior for output files: preserve, ignore. (optional)  (default to "ignore")
            var processingParameterizedShapesEllipseGeneralEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesEllipseCircleEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesTriangleGeneralEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesTriangleIsoscelesEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesQuadrilateralGeneralEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesQuadrilateralRectangleEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesQuadrilateralBulletEnabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesStarN3Enabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesStarN4Enabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesStarN5Enabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var processingParameterizedShapesStarN6Enabled = true;  // bool? | Enable detection and parameterization of this parameterized shape type. (optional)  (default to true)
            var outputFileFormat = "svg";  // string | Output file format to generate. (optional)  (default to svg)
            var outputShapeStacking = "cutouts";  // string | Whether shapes are cut out of each other or stacked atop each other. (optional)  (default to cutouts)
            var outputGroupBy = "none";  // string | Grouping of shapes in output. (optional)  (default to none)
            var outputDrawStyle = "fill_shapes";  // string | How shapes are rendered. (optional)  (default to fill_shapes)
            var outputStrokesStrokeWidth = 1F;  // float? | Width of stroke for shape outlines (when enabled). (optional)  (default to 1F)
            var outputStrokesNonScalingStroke = true;  // bool? | Use non-scaling strokes when drawing shape outlines. (optional)  (default to true)
            var outputStrokesUseOverrideColor = false;  // bool? | Override shape color with a specific color. (optional)  (default to false)
            var outputStrokesOverrideColor = "\"#000000\"";  // string | Color value to override shape stroke color if enabled. Must be in '#RRGGBB' or 'rgba(r,g,b,a)' format. (optional)  (default to "#000000")
            var outputGapFillerEnabled = true;  // bool? | Enable filling small visual gaps caused by vector rendering artifacts. (optional)  (default to true)
            var outputGapFillerNonScalingStroke = true;  // bool? | Use non-scaling strokes for gap filling. (optional)  (default to true)
            var outputGapFillerClip = false;  // bool? | Clip gap filler strokes to shape bounds when stacking shapes. (optional)  (default to false)
            var outputGapFillerStrokeWidth = 2F;  // float? | Width of the gap filler strokes (in output units). (optional)  (default to 2F)
            var outputParameterizedShapesFlatten = false;  // bool? | Whether to flatten detected circles, rectangles, and stars to curves. (optional)  (default to false)
            var outputCurvesLineFitTolerance = 0.1F;  // float? | Maximum allowed error when approximating curves with line segments. (optional)  (default to 0.1F)
            var outputCurvesAllowedQuadraticBezier = true;  // bool? | Allow quadratic Bézier curves in the output. (optional)  (default to true)
            var outputCurvesAllowedCubicBezier = true;  // bool? | Allow cubic Bézier curves in the output. (optional)  (default to true)
            var outputCurvesAllowedCircularArc = true;  // bool? | Allow circular arcs in the output. (optional)  (default to true)
            var outputCurvesAllowedEllipticalArc = true;  // bool? | Allow elliptical arcs in the output. (optional)  (default to true)
            var outputSvgVersion = "svg_1_0";  // string | SVG version to declare in the SVG output. (optional)  (default to svg_1_1)
            var outputSvgFixedSize = false;  // bool? | Whether to fix the SVG dimensions in the output file. (optional)  (default to false)
            var outputSvgAdobeCompatibilityMode = false;  // bool? | Enable Illustrator compatibility by disabling unsupported SVG features. (optional)  (default to false)
            var outputPdfVersion = "PDF_1_4";  // string | PDF version to generate for PDF output. (optional)  (default to PDF_1_4)
            var outputPdfCompressionMode = "None";  // string | Compression method to apply to PDF output streams. (optional)  (default to Deflate)
            var outputEpsVersion = "PS_3_0_EPSF_3_0";  // string | EPS format version for EPS output. (optional)  (default to PS_3_0_EPSF_3_0)
            var outputDxfCompatibilityLevel = "lines_only";  // string | Level of primitive support for DXF output. (optional)  (default to lines_and_arcs)
            var outputBitmapAntiAliasingMode = "anti_aliased";  // string | Anti-aliasing mode for bitmap (PNG) output. (optional)  (default to anti_aliased)
            var outputSizeScale = 3.4F;  // float? | Overall uniform scaling factor for the output image. (optional) 
            var outputSizeWidth = 3.4F;  // float? | Output width, in the selected unit (see output.size.unit). (optional) 
            var outputSizeHeight = 3.4F;  // float? | Output height, in the selected unit (see output.size.unit). (optional) 
            var outputSizeUnit = "none";  // string | Measurement unit for output dimensions. (optional)  (default to none)
            var outputSizeAspectRatio = "preserve_inset";  // string | How to preserve or stretch aspect ratio. (optional)  (default to preserve_inset)
            var outputSizeAlignX = 0.5F;  // float? | Horizontal alignment (0.0 = left, 0.5 = center, 1.0 = right) when aspect ratio is preserved. (optional)  (default to 0.5F)
            var outputSizeAlignY = 0.5F;  // float? | Vertical alignment (0.0 = top, 0.5 = center, 1.0 = bottom) when aspect ratio is preserved. (optional)  (default to 0.5F)
            var outputSizeInputDpi = 3.4F;  // float? | Override the detected DPI of the input image for size computations. (optional) 
            var outputSizeOutputDpi = 3.4F;  // float? | DPI setting for the output image. (optional) 

            try
            {
                // Vectorize an image
                System.IO.Stream result = apiInstance.PostVectorize(image, imageUrl, imageBase64, imageToken, mode, inputMaxPixels, policyRetentionDays, processingMaxColors, processingShapesMinAreaPx, processingPalette, processingColorProfileInput, processingColorProfileOutput, processingParameterizedShapesEllipseGeneralEnabled, processingParameterizedShapesEllipseCircleEnabled, processingParameterizedShapesTriangleGeneralEnabled, processingParameterizedShapesTriangleIsoscelesEnabled, processingParameterizedShapesQuadrilateralGeneralEnabled, processingParameterizedShapesQuadrilateralRectangleEnabled, processingParameterizedShapesQuadrilateralBulletEnabled, processingParameterizedShapesStarN3Enabled, processingParameterizedShapesStarN4Enabled, processingParameterizedShapesStarN5Enabled, processingParameterizedShapesStarN6Enabled, outputFileFormat, outputShapeStacking, outputGroupBy, outputDrawStyle, outputStrokesStrokeWidth, outputStrokesNonScalingStroke, outputStrokesUseOverrideColor, outputStrokesOverrideColor, outputGapFillerEnabled, outputGapFillerNonScalingStroke, outputGapFillerClip, outputGapFillerStrokeWidth, outputParameterizedShapesFlatten, outputCurvesLineFitTolerance, outputCurvesAllowedQuadraticBezier, outputCurvesAllowedCubicBezier, outputCurvesAllowedCircularArc, outputCurvesAllowedEllipticalArc, outputSvgVersion, outputSvgFixedSize, outputSvgAdobeCompatibilityMode, outputPdfVersion, outputPdfCompressionMode, outputEpsVersion, outputDxfCompatibilityLevel, outputBitmapAntiAliasingMode, outputSizeScale, outputSizeWidth, outputSizeHeight, outputSizeUnit, outputSizeAspectRatio, outputSizeAlignX, outputSizeAlignY, outputSizeInputDpi, outputSizeOutputDpi);
                Debug.WriteLine(result);
            }
            catch (ApiException  e)
            {
                Debug.Print("Exception when calling VectorizationApi.PostVectorize: " + e.Message);
                Debug.Print("Status Code: " + e.ErrorCode);
                Debug.Print(e.StackTrace);
            }
        }
    }
}
```

#### Using the PostVectorizeWithHttpInfo variant
This returns an ApiResponse object which contains the response data, status code and headers.

```csharp
try
{
    // Vectorize an image
    ApiResponse<System.IO.Stream> response = apiInstance.PostVectorizeWithHttpInfo(image, imageUrl, imageBase64, imageToken, mode, inputMaxPixels, policyRetentionDays, processingMaxColors, processingShapesMinAreaPx, processingPalette, processingColorProfileInput, processingColorProfileOutput, processingParameterizedShapesEllipseGeneralEnabled, processingParameterizedShapesEllipseCircleEnabled, processingParameterizedShapesTriangleGeneralEnabled, processingParameterizedShapesTriangleIsoscelesEnabled, processingParameterizedShapesQuadrilateralGeneralEnabled, processingParameterizedShapesQuadrilateralRectangleEnabled, processingParameterizedShapesQuadrilateralBulletEnabled, processingParameterizedShapesStarN3Enabled, processingParameterizedShapesStarN4Enabled, processingParameterizedShapesStarN5Enabled, processingParameterizedShapesStarN6Enabled, outputFileFormat, outputShapeStacking, outputGroupBy, outputDrawStyle, outputStrokesStrokeWidth, outputStrokesNonScalingStroke, outputStrokesUseOverrideColor, outputStrokesOverrideColor, outputGapFillerEnabled, outputGapFillerNonScalingStroke, outputGapFillerClip, outputGapFillerStrokeWidth, outputParameterizedShapesFlatten, outputCurvesLineFitTolerance, outputCurvesAllowedQuadraticBezier, outputCurvesAllowedCubicBezier, outputCurvesAllowedCircularArc, outputCurvesAllowedEllipticalArc, outputSvgVersion, outputSvgFixedSize, outputSvgAdobeCompatibilityMode, outputPdfVersion, outputPdfCompressionMode, outputEpsVersion, outputDxfCompatibilityLevel, outputBitmapAntiAliasingMode, outputSizeScale, outputSizeWidth, outputSizeHeight, outputSizeUnit, outputSizeAspectRatio, outputSizeAlignX, outputSizeAlignY, outputSizeInputDpi, outputSizeOutputDpi);
    Debug.Write("Status Code: " + response.StatusCode);
    Debug.Write("Response Headers: " + response.Headers);
    Debug.Write("Response Body: " + response.Data);
}
catch (ApiException e)
{
    Debug.Print("Exception when calling VectorizationApi.PostVectorizeWithHttpInfo: " + e.Message);
    Debug.Print("Status Code: " + e.ErrorCode);
    Debug.Print(e.StackTrace);
}
```

### Parameters

| Name | Type | Description | Notes |
|------|------|-------------|-------|
| **image** | **System.IO.Stream****System.IO.Stream** | Binary file upload of the image to vectorize. Accepts .bmp, .gif, .jpeg, .png, or .tiff files. | [optional]  |
| **imageUrl** | **string** | URL to fetch the input image from for vectorization. | [optional]  |
| **imageBase64** | **byte[]** | Base64-encoded string of the input image. Maximum size 1 megabyte. | [optional]  |
| **imageToken** | **string** | An Image Token returned from an earlier vectorization call with policy.retention_days &gt; 0. | [optional]  |
| **mode** | **string** | Mode of operation, useful during integration work. | [optional] [default to production] |
| **inputMaxPixels** | **int?** | Maximum input image size (width × height in pixels) before resizing. | [optional] [default to 2097252] |
| **policyRetentionDays** | **int?** | Number of days to retain the uploaded image and its results for re-use. | [optional] [default to 0] |
| **processingMaxColors** | **int?** | Maximum number of colors allowed in the vectorization result. 0 means unlimited. | [optional] [default to 0] |
| **processingShapesMinAreaPx** | **float?** | Minimum shape area (in pixels) to keep in the result; smaller shapes are discarded. | [optional] [default to 0.125F] |
| **processingPalette** | **string** | Palette remapping and color control, using &#39;[color][-&gt; remapped][~ tolerance];&#39; format. | [optional]  |
| **processingColorProfileInput** | **string** | How to handle ICC profiles embedded in input images. | [optional] [default to ignore] |
| **processingColorProfileOutput** | **string** | ICC profile behavior for output files: preserve, ignore. | [optional] [default to &quot;ignore&quot;] |
| **processingParameterizedShapesEllipseGeneralEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesEllipseCircleEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesTriangleGeneralEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesTriangleIsoscelesEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesQuadrilateralGeneralEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesQuadrilateralRectangleEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesQuadrilateralBulletEnabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesStarN3Enabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesStarN4Enabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesStarN5Enabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **processingParameterizedShapesStarN6Enabled** | **bool?** | Enable detection and parameterization of this parameterized shape type. | [optional] [default to true] |
| **outputFileFormat** | **string** | Output file format to generate. | [optional] [default to svg] |
| **outputShapeStacking** | **string** | Whether shapes are cut out of each other or stacked atop each other. | [optional] [default to cutouts] |
| **outputGroupBy** | **string** | Grouping of shapes in output. | [optional] [default to none] |
| **outputDrawStyle** | **string** | How shapes are rendered. | [optional] [default to fill_shapes] |
| **outputStrokesStrokeWidth** | **float?** | Width of stroke for shape outlines (when enabled). | [optional] [default to 1F] |
| **outputStrokesNonScalingStroke** | **bool?** | Use non-scaling strokes when drawing shape outlines. | [optional] [default to true] |
| **outputStrokesUseOverrideColor** | **bool?** | Override shape color with a specific color. | [optional] [default to false] |
| **outputStrokesOverrideColor** | **string** | Color value to override shape stroke color if enabled. Must be in &#39;#RRGGBB&#39; or &#39;rgba(r,g,b,a)&#39; format. | [optional] [default to &quot;#000000&quot;] |
| **outputGapFillerEnabled** | **bool?** | Enable filling small visual gaps caused by vector rendering artifacts. | [optional] [default to true] |
| **outputGapFillerNonScalingStroke** | **bool?** | Use non-scaling strokes for gap filling. | [optional] [default to true] |
| **outputGapFillerClip** | **bool?** | Clip gap filler strokes to shape bounds when stacking shapes. | [optional] [default to false] |
| **outputGapFillerStrokeWidth** | **float?** | Width of the gap filler strokes (in output units). | [optional] [default to 2F] |
| **outputParameterizedShapesFlatten** | **bool?** | Whether to flatten detected circles, rectangles, and stars to curves. | [optional] [default to false] |
| **outputCurvesLineFitTolerance** | **float?** | Maximum allowed error when approximating curves with line segments. | [optional] [default to 0.1F] |
| **outputCurvesAllowedQuadraticBezier** | **bool?** | Allow quadratic Bézier curves in the output. | [optional] [default to true] |
| **outputCurvesAllowedCubicBezier** | **bool?** | Allow cubic Bézier curves in the output. | [optional] [default to true] |
| **outputCurvesAllowedCircularArc** | **bool?** | Allow circular arcs in the output. | [optional] [default to true] |
| **outputCurvesAllowedEllipticalArc** | **bool?** | Allow elliptical arcs in the output. | [optional] [default to true] |
| **outputSvgVersion** | **string** | SVG version to declare in the SVG output. | [optional] [default to svg_1_1] |
| **outputSvgFixedSize** | **bool?** | Whether to fix the SVG dimensions in the output file. | [optional] [default to false] |
| **outputSvgAdobeCompatibilityMode** | **bool?** | Enable Illustrator compatibility by disabling unsupported SVG features. | [optional] [default to false] |
| **outputPdfVersion** | **string** | PDF version to generate for PDF output. | [optional] [default to PDF_1_4] |
| **outputPdfCompressionMode** | **string** | Compression method to apply to PDF output streams. | [optional] [default to Deflate] |
| **outputEpsVersion** | **string** | EPS format version for EPS output. | [optional] [default to PS_3_0_EPSF_3_0] |
| **outputDxfCompatibilityLevel** | **string** | Level of primitive support for DXF output. | [optional] [default to lines_and_arcs] |
| **outputBitmapAntiAliasingMode** | **string** | Anti-aliasing mode for bitmap (PNG) output. | [optional] [default to anti_aliased] |
| **outputSizeScale** | **float?** | Overall uniform scaling factor for the output image. | [optional]  |
| **outputSizeWidth** | **float?** | Output width, in the selected unit (see output.size.unit). | [optional]  |
| **outputSizeHeight** | **float?** | Output height, in the selected unit (see output.size.unit). | [optional]  |
| **outputSizeUnit** | **string** | Measurement unit for output dimensions. | [optional] [default to none] |
| **outputSizeAspectRatio** | **string** | How to preserve or stretch aspect ratio. | [optional] [default to preserve_inset] |
| **outputSizeAlignX** | **float?** | Horizontal alignment (0.0 &#x3D; left, 0.5 &#x3D; center, 1.0 &#x3D; right) when aspect ratio is preserved. | [optional] [default to 0.5F] |
| **outputSizeAlignY** | **float?** | Vertical alignment (0.0 &#x3D; top, 0.5 &#x3D; center, 1.0 &#x3D; bottom) when aspect ratio is preserved. | [optional] [default to 0.5F] |
| **outputSizeInputDpi** | **float?** | Override the detected DPI of the input image for size computations. | [optional]  |
| **outputSizeOutputDpi** | **float?** | DPI setting for the output image. | [optional]  |

### Return type

**System.IO.Stream**

### Authorization

[basicAuth](../README.md#basicAuth)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: image/svg+xml, application/postscript, application/pdf, application/dxf, image/png, application/json


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | The vectorized image file. |  * Content-Disposition - Suggested filename for the generated result. <br>  * Content-Encoding - May be gzip for SVG, EPS, or DXF responses when the request allows gzip encoding. <br>  * X-Image-Token - Returned by vectorize when policy.retention_days is greater than 0. <br>  * X-Credits-Charged - Credits charged for the request. This is 0 for test requests. <br>  * X-Credits-Calculated - Returned for test requests to show the credits that would have been charged for the equivalent non-test request. <br>  |
| **400** | Invalid request parameters, image input, URL fetch, or Image Token. |  -  |
| **401** | Missing or invalid API credentials. |  * WWW-Authenticate - HTTP Basic authentication challenge returned with 401 responses. <br>  |
| **402** | The account does not have an API subscription, is past due, or is out of credits. |  -  |
| **413** | The uploaded image, fetched image, or requested PNG output is too large. |  -  |
| **429** | Rate limit exceeded. Back off before retrying. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |
| **500** | Unexpected internal error. |  -  |
| **503** | Temporary overload or internal processing timeout. Retry later. |  * Retry-After - Number of seconds to wait before retrying, when provided. <br>  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

