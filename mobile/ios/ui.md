iOS user interface design and development
=========================================

## Properties not listed in IB

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
