# JavaAPI

Java API, a wrapper SDK of FIX API, provides clients with a fully functioning programmable API into the FXCM trading platform, including streaming live price, get historical price and live trades. It is a scalable, light and robust which compatible on any Java-compliant operating system.

## How to access the JAVA JAR files:
1) Click on the link below and download the [zip file]https://apiwiki.fxcorporate.com/api/java/trading_sdk.zip
2) Extract the fxcm-api folder to a location of your choice
3) Rename fxcm-api.jar and fxmsg.jar to fxcm-api.zip and fxmsg.zip
4) Extract these files to a location of your choice
You now have access to the contents of the JAR files.

## Netbeans Setup:
The FXCM-API-Offerings readme page points to **Netbeans** as an IDE to use with the **Java Trading Api**, but the FXCM-Java/Java-API-Example directory only contains a couple of Eclipse related files. This is how you can setup a Netbeans project to use the examples. There are two basic methods. You can either copy the files into a new Java Application project or you can clone FXCM-API-Offerings and tell Netbeans to create a Java Project with Existing Sources. Either way, we will setup a Library to reference the fxcm-api and fxmsg JAR files.

### FXCM Java API Library:
1. Download the trading_sdk.zip file listed in the **JAVA JAR files** section above and extract it to the location of your choice on your computer.
1. Choose Libraries from the Netbeans Tools menu.
1. Click the New Library button and give it a name like FXCM API. The type should be Class Libraries. Click OK.
1. With your new library selected, you are going to update the Classpath, Sources, and Javadoc tabs as follows:
 * **Classpath** Click the Add JAR/Folder button and navigate to the trading_sdk/fxcm-api directory you extracted and select both the fxcm-api.jar and fxmsg.jar files.
 * **Sources** Click the Add JAR/Folder button on the Sources tab and navigate to the trading_sdk/fxcm-api/src directory and click Add JAR/Folder.
 * **Javadoc** Click teh Add ZIP/Folder button on the Javadoc tab and navigate to the trading_sdk/fxcm-api/javadoc directory and click Add ZIP/Folder.
1. Your library is now ready to include in your project. Click OK.

### New Java Application:

If you don't care about keeping in sync with this project on GitHub, you can create a new Java Application and copy/paste the source code into the project and work from there.

1. File > New Project or New Project button or Ctr+Shift+N
1. Choose the Java category and Java Application and click Next.
1. Give it a name, verify the location, and your choice on using a *Dedicated Folder for Storing Libraries*. You don't need a main class created, so uncheck that.
1. Create a new Java Class. Name it the same as the examples, either JavaFixHistoryMiner or JavaFixTrader. The source doesn't specify a package so either don't specify one or if you use one, like com.fxcm.example, be sure to leave the package declaration at the top of the file when you paste in the contents.
1. View the raw version of the file on GitHub. Select all and copy, then paste into your new Java class in Netbeans, replacing everything except maybe the package declaration.
1. Right-click on your project's Libraries folder and choose Add Library. Find the FXCM API library you created and click Add Library.

### New Java Project with Existing Sources:

If you would like to be able to update with the latest from GitHub, or if you want to Fork and track your own changes, possibly contributing back via pull request, then use this method instead of the previous one to setup Netbeans.

1. Clone the FXCMAPI/FXCM-API-Offerings repository or optionally your fork of it at youruser/FXCM-API-Offerings to a location of your choice on your computer.
1. File > New Project or New Project button or Ctr+Shift+N
1. Choose the Java category and Java Project with Existing Sources and click Next.
1. Give it a name, verify the location, and your choice on using a *Dedicated Folder for Storing Libraries*. The default build script name of build.xml is fine.
1. Click Next and click the Add Folder button.
1. Browse to the FXCM-API-Offerings\FXCM-Java\Java-API-Example directory and click Open.
1. Verify the two .java files are selected and finish.
1. Right-click on your project's Libraries folder and choose Add Library. Find the FXCM API library you created and click Add Library.

## Real Case Study:
1. How to build Rsi signal and back testing using FXCM Java API. <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/FXCM_Java_API_Tutorial_RsiSignal_Strategy.zip" target="_blank"> click here</a>
2. Learn how to build and backtest CCI Oscillator strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/CCIOscillatorStrategy-2.zip">here</a>.
3. Lean how to build and back test Breakout strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/BreakOutStrategy_JavaAPI.zip">here</a>. 
4. Lean how to build and back test Range Stochastic Strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/RangeStochasticStrategy.zip">here</a>. 
5. Lean how to build and back test Mean Reversion Strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/MeanReversionStrategy.zip">here</a>. 