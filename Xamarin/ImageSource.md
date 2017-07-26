# Image Source

[ImageSource](https://developer.xamarin.com/api/type/Xamarin.Forms.ImageSource/) is used with the `Image.Source` property within Xamarin.Forms. 

### Local Files

To display local files correctly (at least on iOS), the `Image.Source` property must be bound to a property that returns an `ImageSource.FromFile` value.

```csharp
public ImageSource Thumbnail
{
    get
    {
        return ImageSource.FromFile("/path/to/local/file");
    }
}
```
