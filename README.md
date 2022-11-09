# visx-swiftui-sdk-ios

VIS.X® is a new and unique kind of advertising technology that enables efficient execution of media and high-impact ad products at scale. VIS.X® wraps the inventory in a holistic auction offering all available products in one transaction to buyers, consequently optimizing the bidstream. YOC has developed this platform to unlock the real value of digital advertising – making VIS.X® the go-to-platform for high-impact programmatic advertising.

# Intro #

VisxSDK offers SwiftUI support. There are two ways to use it in the SwiftUI project.
1. Use VisxSDK and create your own wrapper (UIViewRepresentable/UIViewControllerRepresentable), or
2. Use VisxSwiftUISDK (recommended), which is ready to be used right away.



# Getting Started #

Adding the SDK is via Cocoapods.
To use it in your project simply add VisxSwiftUISDK pod to your targets.
#
	pod 'VisxSwiftUISDK' 
#

and in terminal execute 'pod install' command.

Activation, GDPR and User Tracking is exactly the same as VisxSDK, see Getting Started (https://support.yoc.com/ios-sdk/getting-started/).



# Integration #

# Universal/Banner #

1. Import VisxSwiftUISDK
 
After you have installed and activated the SDK you can import VisxSwiftUISDK in you "View" and you are ready to use it.
# 
	import VisxSwiftUISDK 
#


2. Initialise VisxView for an ad request

VisxView is a SwiftUI View. Just create an instance
#
	let visxView = VisxView(adUnitId: "123456", 
                            domain: "domain-of-you-app-ads-txt.com", 
                            size: .kSmartphoneBanner300x150, 
                            universal: true)
#

and use it in the "body" of your "View"
#
    var body: some View {
        ScrollView {
            ForEach(1..<30) { row in
                if row == 10 {
                    visxView
                }
                Text("Sample Text")
            }
        }
    }
#

Instead of using Swift delegate methods, VisxView has a function that can receive all Visx events (visxAdViewDidInitialize, visxAdViewSizeChange etc..) which are available for Swift (https://support.yoc.com/ios-sdk/annex/visx-adview-delegates/)
#
	visxView.onEvent { visxEvent in
		// visxEvent is a VisxEvent enum of type string
	}
#

Example of enum VisxEvents
#
	public enum VisxEvents: String {
    	case visxAdViewDidInitialize
    	case visxAdViewSizeChange
    	case visxAdViewEffectChange
    	case visxLandingPageOpened
    	case visxAdViewClosed
    	case visxAdViewClicked
    	case visxAdVideoFinished
    	case visxAdRequestStarted
    	case visxAdInterstitialClosed
    	case visxAdInterstitialWillBeClosed
    	case visxAdResponseReceived
    	case visxAdFailedWithError
    	case appShouldResumeFromAd
    	case appShouldSuspendForAd
    	case visxAdViewDeallocated
	}
#

3. Optional: Set the AnchorFrame for VisxView

In case of complex app layouts you may need to provide the viewable part of the View, the VisxView is located, in manually.

#
    let visxView = VisxView(adUnitId: "123456",
                            domain: "domain-of-you-app-ads-txt.com",
                            size: .kSmartphoneBanner300x150,
                            universal: true,
                            anchorFrame: CGRect(x: 0, y: 132, width: 393, height: 720))
#

# Interstitial #

1. Import VisxSwiftUISDK
 
After you have installed and activated the SDK you can import VisxSwiftUISDK in you "View" and you are ready to use it.

# 
	import VisxSwiftUISDK 
#

2. Initialise VisxInterstitial manager for an ad request

# 
	let interstitial = VisxInterstitial(adUnitId: "123456", domain: "domain-of-you-app-ads-txt.com")
#

After creating the instance of VisxInterstitial manager, there are two functions that you can call on it
- loadAd(), it does the network request to load the interstitial ad
- showAd(), after its loaded we can present it on screen.

# 
    var body: some View {
        VStack {
            Button("Load Ad") {
                interstitial.loadAd()
            }
            Button("Show Ad") {
                interstitial.showAd()
            }
        }
    }
#


# Custom Features #

Custom features that are available for Swift are also available for SwiftUI.
Check this link for explanation what are they used for (https://support.yoc.com/ios-sdk/integration/custom-features/)
Only difference is implementation, you can see below example.

1. Setting Keyword Targeting

# 
    let visxView = VisxView(adUnitId: "123456",
                            domain: "domain-of-you-app-ads-txt.com",
                            size: .kSmartphoneBanner300x150,
                            universal: true,
                            loadWithCustomTargetingParameters: ["age": "40", "gender": "male"])
#

2. Interstitial: Setting Background Color

# 
    let interstitial = VisxInterstitial(adUnitId: "123456",
                                        domain: "domain-of-you-app-ads-txt.com",
                                        backgroundColor: .pink)
#

3. Banner: Setting Advertisement Label

# 
    let visxView = VisxView(adUnitId: "123456",
                            domain: "domain-of-you-app-ads-txt.com",
                            size: .kSmartphoneBanner300x150,
                            universal: true,
                            advertisingLabelText: "Sample Text")
#


This custom features are optional and can be omitted if not needed. 
