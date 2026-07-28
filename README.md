# UgoForms

UgoForms is a powerful, ready-to-use SwiftUI component that allows users to seamlessly view, fill out, and export PDF forms directly within your iOS app. 

It provides an intuitive interface for editing PDFs and a simple API for developers to retrieve the filled document data.

## Features

- **SwiftUI Native:** Built from the ground up to integrate perfectly with SwiftUI apps.
- **Easy Integration:** Just drop in `UgoPDFFillerView` and provide a local PDF URL.
- **Built-in Export:** Callback mechanism to easily handle the filled PDF data once the user is done.

## Requirements

- iOS 16.0+
- Swift 5.7+
- Xcode 16+

## Installation

### Swift Package Manager

You can integrate `UgoForms` into your project using Swift Package Manager.

1. In Xcode, go to **File** > **Add Packages...**
2. Enter the repository URL: `https://github.com/YugeeLabs/ugo-forms-ios-spm.git`
3. Choose the exact version or up to next major version.
4. Click **Add Package**.

## Usage

Using `UgoForms` is incredibly straightforward. Import the library and use `UgoPDFFillerView` in your SwiftUI view hierarchy. 

Here is a basic implementation:

```swift
import SwiftUI
import UgoForms

struct ContentView: View {
    // The URL to the local PDF file you want the user to fill
    @State private var pdfURL: URL?
    
    // A binding to trigger export programmatically if needed
    @State private var triggerExport = false

    var body: some View {
        if let url = pdfURL {
            UgoPDFFillerView(
                url: url,
                exportTrigger: $triggerExport,
                onClose: {
                    // Handle user closing the PDF viewer
                    pdfURL = nil
                },
                onExportPDF: { filledPdfData in
                    // Handle the exported PDF data (e.g., save to disk, upload, or share)
                    saveAndShare(data: filledPdfData)
                }
            )
        } else {
            Button("Open PDF Form") {
                // Set your local PDF URL here
                // pdfURL = ... 
            }
        }
    }
    
    private func saveAndShare(data: Data) {
        // Example logic to save data and present a share sheet
    }
}
```

### Parameters

- `url`: The local file `URL` pointing to the PDF document.
- `exportTrigger`: A `@Binding<Bool>` that you can toggle to force an export programmatically from outside the view.
- `onClose`: A closure executed when the user taps the close button or finishes editing.
- `onExportPDF`: A closure returning a `Data` object representing the newly filled PDF. Use this to save the file or share it.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
