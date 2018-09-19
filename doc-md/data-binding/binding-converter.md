## Value Converter
If you want to bind value of one type and then present it slightly differently, you need a value converter.
**A binding implicitly uses a default converter that tries to do a type conversion between the source value and the target value. If a conversion cannot be made, the default converter returns null.**
If you want to associate a custom value converter with a binding, you should create a class that implements the IValueConverter interface
```
public interface IValueConverter {
	Convert(Object, Type, Object, CultureInfo)
	ConvertBack(Object, Type, Object, CultureInfo)
}
```

#### Some Use Cases:
* You have a numeric value but you want to show zero values in one way and positive numbers in another way
* You want to check a CheckBox based on a value, but the value is a string like "yes" or "no" instead of a Boolean value
* You have a file size in bytes but you wish to show it as bytes, kilobytes, megabytes or gigabytes based on how big it is
* Generate an image for an ImageSource, based on the value, like a green sign for true or a red sign for false


#### Explanation with Example
```
<Rectangle Fill="Green"/)
```
or
```
<Rectangle Fill="#00FF00"/)
```
you might be fooled into thinking that the `Fill` property is of type `Color` but actually of type `Brush` and the XAML parser is performing some cunning type conversions in order to make the above markup work.
The solution to this problem of binding a `Color` to the `Fill` property is to create a value converter:
```
public class ColorToBrushConverter : IValueConverter
{
  public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
  {
    if (value is Color)
    {
      return new SolidColorBrush((Color)value);
    }
    return null;
  }

  public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
  {
    throw new Exception("The method or operation is not implemented.");
  }
}
```

Which can be used as follows:
```
<Rectangle Fill="{Binding Path=MyColorProperty,
                                  Converter={StaticResource ColorToBrushConverter}} "/)
```

## UniversalValueConverter 
```
public class UniversalValueConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
    {
        // obtain the conveter for the target type
        TypeConverter converter = TypeDescriptor.GetConverter(targetType);

        try
        {
            // determine if the supplied value is of a suitable type
            if (converter.CanConvertFrom(value.GetType()))
            {
                // return the converted value
                return converter.ConvertFrom(value);
            }
            else
            {
                // try to convert from the string representation
                return converter.ConvertFrom(value.ToString());
            }
        }
        catch (Exception)
        {
            return value;
        }

    }

    public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
    {
        throw new NotImplementedException();
    }
}
```

**Usage: String to  Color**
```
<TextBox x:Name="colorTextBox" Text="Red"/>

<Rectangle Fill="{Binding ElementName=colorTextBox, Path=Text, Converter={StaticResource UniversalValueConverter}}"/>
```

See: [Details](https://blog.scottlogic.com/2010/07/09/a-universal-value-converter-for-wpf.html)
