iOS user interface design and development
=========================================

## Making properties listed in IB

Certain properties of UI elements are not accessible in IB by default (such as the `shadowRadius`). It is possible to subclass/extend a UI element to make a property
accessible through IB. For example, here's how one could configure the corner radius of a view:

```
    extension UIView {
    @IBInspectable var cornerRadius: CGFloat {
        get {
            return layer.cornerRadius
        }
        set {
            layer.cornerRadius = newValue
            layer.masksToBounds = newValue > 0
        }
    }
```

It's also possible to simply add a custom properties that's not related to an existing view property so that it can be configured through IB, and to make a whole
subclass of an `NSView` or `UIView` by annotating them as `@IDesignable`:

```
    @IBDesignable
    class MyCustomView: UIView {

    }
```
