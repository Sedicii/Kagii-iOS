# Appearance

Defining the appearance. This is way to define your own appearance.

```swift
Kagii.userInterface.appearance = ClientAppearance.appearance
```

The following code is the Appearance definition written in Swift. You should take into account that all these parameters
are optional, and they have a default value except for `Footer.logo` which is optional but if you do not defined it, this
logo won't appear.

```swift
import UIKit

public struct KagiiAppearance {

    public enum FontTransformation {
        case none
        case uppercase
        case lowercase
        case capitalized
        case smallCaps
    }

    public enum FontWeight {
        case lighter
        case light
        case regular
        case bold
        case bolder
    }

    public enum Elevation: Int {
        case none
        case verySmall
        case small
        case medium
        case high
        case veryHigh
    }

    public struct ColorPalette {
        public var main: UIColor = .white
        public var contrastText: UIColor = .black
    }

    public struct Title {
        public var weight: FontWeight = .regular
        public var transformation: FontTransformation = .none
    }

    public struct CloseButton {
        public var palette = ColorPalette()
    }

    public struct Button {
        public var borderRadius: CGFloat = 8.0
        public var elevation: Elevation = .none
        public var fontTransformation: FontTransformation = .uppercase
    }

    public struct LinkButton {
        public var palette = ColorPalette(contrastText: Asset.colorSplitComplentaryLigth.color)
    }

    public struct TextField {
        public var borderRadius: CGFloat = 4.0
        public var elevation: Elevation = .none
        public var palette = ColorPalette(
            main: Asset.colorTextFieldMain.color,
            contrastText: Asset.colorTextFieldContrastText.color
        )
    }

    public struct ListView {
        public var borderRadius: CGFloat = 0.0
        public var elevation: Elevation = .none
        public var background = ColorPalette(main: Asset.colorSediciiGray.color, contrastText: .white)
    }

    public struct Theme {
        public var primary = ColorPalette(main: Asset.colorPrimary.color, contrastText: Asset.colorSediciiGray.color)
        public var secondary = ColorPalette(main: Asset.colorSecondary.color, contrastText: .white)
        public var error = ColorPalette(main: Asset.colorError.color, contrastText: Asset.colorError.color)
    }

    public struct Header {
        public var palette = ColorPalette()
        public var logo = UIImage(asset: Asset.imageSediciiLogo)
        public var closeButton = CloseButton()
        public var title = Title(weight: .bold, transformation: .smallCaps)
        public var subtitle = Title(weight: .light, transformation: .smallCaps)
    }

    public struct Footer {
        public var logo: UIImage?
    }

    public struct Icons {
        public var processing = UIImage(asset: Asset.imageProcessing)
        public var uploading = UIImage(asset: Asset.imageUploading)
        public var authFactorPhoneNumber = UIImage(asset: Asset.imageAuthFactorPhoneNumber)
        public var authFactorEmail = UIImage(asset: Asset.imageAuthFactorEmail)
        public var validationFirst = UIImage(asset: Asset.imageValidationCompletedFirst)
        public var validationSecond = UIImage(asset: Asset.imageValidationCompletedSecond)
        public var finished = UIImage(asset: Asset.imageFinish)
    }

    public var contentPalette: ColorPalette
    public var theme: Theme
    public var button: Button
    public var linkButton: LinkButton
    public var textField: TextField
    public var listView: ListView
    public var header: Header
    public var footer: Footer
    public var icons: Icons

    public init() {
        contentPalette = ColorPalette()
        theme = Theme()
        button = Button()
        linkButton = LinkButton()
        textField = TextField()
        listView = ListView()
        header = Header(palette: theme.secondary, closeButton: CloseButton(palette: theme.secondary))
        footer = Footer()
        icons = Icons()
    }

}
```

#### Example of appearance

```swift
import Kagii
import UIKit

struct ClientAppearance {

    private init() {}

    static let appearance: KagiiAppearance = {
        var appearance = KagiiAppearance()

        appearance.button.borderRadius = 8.0
        appearance.button.elevation = .none
        appearance.button.fontTransformation = .uppercase

        appearance.contentPalette.main = .white
        appearance.contentPalette.contrastText = .black

        appearance.theme.primary.main = UIColor(asset: Asset.colorPrimary)
        appearance.theme.primary.contrastText = .white
        appearance.theme.secondary.main = UIColor(asset: Asset.colorPrimary)
        appearance.theme.secondary.contrastText = .white

        appearance.header.logo = UIImage(asset: Asset.sediciiLogo)
        appearance.header.palette = appearance.contentPalette
        appearance.header.title.transformation = .none
        appearance.header.title.weight = .regular
        appearance.header.subtitle.transformation = .none
        appearance.header.subtitle.weight = .light

        appearance.icons.processing = UIImage(asset: Asset.customImageProcessing)

        appearance.listView.background = appearance.theme.secondary
        appearance.listView.borderRadius = 8.0
        appearance.listView.elevation = .none

        appearance.textField.borderRadius = 8.0
        appearance.textField.elevation = .none
        appearance.textField.palette.main = appearance.contentPalette.main
        appearance.textField.palette.contrastText = appearance.contentPalette.contrastText

        return appearance
    }()

}
```
