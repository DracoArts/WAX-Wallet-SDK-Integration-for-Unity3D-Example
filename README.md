
# Welcome to DracoArts

![Logo](https://dracoarts-logo.s3.eu-north-1.amazonaws.com/DracoArts.png)




# WWAX-Wallet-SDK-Integration-for-Unity3D-Example
The WAX Wallet SDK for Unity is a powerful toolkit designed to bridge Unity-based games and applications with the WAX (Worldwide Asset eXchange) blockchain, enabling seamless integration of decentralized features such as NFTs, token transactions, wallet authentication, and smart contract interactions. By leveraging this SDK, developers can incorporate blockchain functionality without deep expertise in Web3 protocols, allowing them to focus on building immersive gaming experiences while still benefiting from WAX’s fast, fee-less transactions and NFT infrastructure.

## 1. Wallet Connectivity & User Authentication

### WAX Cloud Wallet (WCW) Integration 
- Users can log in via WAX’s streamlined wallet system with just a few clicks, eliminating complex private key management.

### External Wallet Support 
- Compatible with Anchor, Scatter, and other WAX-compatible wallets for broader user accessibility.

### Auto-Login & Session Persistence 
- Maintains user sessions across gameplay sessions, reducing repeated sign-in requests.

### Account Verification 
 - Securely confirm wallet ownership before allowing blockchain interactions.

## 2. Token & NFT Management
### WAX Token Transactions 
- Send and receive WAXP tokens (the native currency of the WAX blockchain) between players or for in-game purchases.

### NFT Operations 

#### Fetch NFTs 
- Retrieve a user’s NFT inventory from their WAX wallet.

- Transfer NFTs – Enable peer-to-peer or marketplace NFT trades.

- Mint & Burn NFTs – Create or destroy in-game assets on-chain.

 ### AtomicAssets Integration 
 - Built-in support for WAX’s AtomicHub NFT standard, making it easy to interact with popular marketplaces.

##  3 Smart Contract Interactions
### Execute Custom Actions 
- Call smart contract methods (e.g., staking, crafting, or in-game item upgrades) directly from Unity.

### Transaction Builder 
- Simplifies complex multi-action transactions (e.g., buying an NFT and equipping it in-game in one step).

### Gas-Free Transactions 
 - Leverages WAX’s Resource Exchange (REX) for fee-less transactions, improving user experience.

## 4. Cross-Platform Compatibility
- Supports WebGL, PC (Windows/macOS), and Mobile (iOS/Android) deployments.

- Adaptable to different wallet connection methods (e.g., QR codes for mobile, pop-ups for WebGL).

## 5. Event Handling & Callbacks
### Transaction Status Tracking 
- Real-time updates on pending, successful, or failed transactions.

### Wallet State Monitoring 
Detect wallet disconnections or account changes dynamically.

# Benefits for Game Developers
## 1. Simplified Blockchain Integration
- No need to write low-level WAX RPC calls—pre-built methods handle authentication, transactions, and NFT operations.

- Abstracts away cryptographic complexities, making it accessible even for developers new to Web3.

## 2. Enhanced Player Experience
### Seamless Logins 
-  Players can use their existing WAX wallet without additional registrations.

### True Digital Ownership 
 - Players own their in-game assets as tradable NFTs.

### Play-to-Earn (P2E) Ready 
-  Easily integrate token rewards, NFT loot drops, and decentralized economies.

## 3. Security & Compliance
###  Non-Custodial 
- Private keys remain with the user (no centralized storage risk).

### Anti-Fraud Mechanisms 
- Built-in transaction validation to prevent unauthorized actions.

## 4. Scalability & Performance
 #### Optimized for high
- throughput gaming environments (WAX handles thousands of transactions per second).

 #### Batch Transactions 
 - Combine multiple actions to reduce blockchain load.


#  Installation
- Requires Unity 2019.1+ with .NET 4.x+ Runtime

## This package can be included into your project by either:

- Installing the package via Unity's Package Manager (UPM) in the editor (recommended).

Importing the .unitypackage which you can download here.[here](https://github.com/liquiidio/cloudwalletunity/releases)

- Manually add the files from the repo.

## Dependencies

None of the dependencies is contained in this Package and no matter which installation method you choose, you have to install it manually in addition to this Package.

## EosSharp

- EosSharp is a library containing the necessary functionallity to serialize and deserialize Actions, Transactions, Blocks and other Data

- In addition it contains the necessary functionallity for all kinds of cryptographic operations

- Lastly it contains the functionallity allowing you and the AnchorLink-Library to access EOSIO or LEAP-based Nodes via their APIs.

## Follow the Instructions in [EosSharp](https://liquiidio.gitbook.io/unity-plugin-suite/v/eossharp/installation)

- Or install the Package directly via UPM

- Installing via Unity Package Manager (UPM).

## In your Unity project:

- Open the Package Manager Window/Tab

- Click Add Package From Git URL

Enter URL: 

             https://github.com/liquiidio/EosSharp.git#upm

## 1. Recommended - Installing via Unity Package Manager (UPM).
In your Unity project:

- Open the Package Manager Window/Tab

- Click Add Package From Git URL

Enter URL: 

    https://github.com/liquiidio/cloudwalletunity.git#upm

## 2. Importing the Unity Package.

- Download the [UnityPackagehere](https://github.com/liquiidio/cloudwalletunity/releases)

### Then in your Unity project:

- Open up the import a custom package window

- Navigate to where you downloaded the file and open it.

- Check all the relevant files needed (if this is a first time import, just select ALL) and click on import.

## 3. Install manually.

- Download the project .[here](https://github.com/liquiidio/cloudwalletunity/releases)

- Then in your Unity project, copy the sources from WCWUnity into your Unity Assets directory.


# WebGL Installation
- WebGL builds will require the index.html file to be customised.

- Download the full customised file [here](https://github.com/liquiidio/UnityPluginSuiteGitbook/blob/WcwUnity/custom/downloads/index.html)

- Important! waxjs.js needs to be included in your build, next to the customised html file and needs to be loaded by your html file. Download waxjs.js [here](https://github.com/worldwide-asset-exchange/waxjs/tree/develop/dist-web)

- Ensure that this line is added to make websockets work.   

       window.unityInstance = unityInstance;
### Final script should have this included

        script.onload = () => {
        createUnityInstance(canvas, config, (progress) => {
          progressBarFull.style.width = 100 * progress + "%";
          }).then((unityInstance) => {
	  
	  // !!! IMPORTANT
	  window.unityInstance = unityInstance; // <-- THIS LINE MUST BE ADDED TO ENSURE WEBSOCKETS WORK!!!
          // !!! IMPORTANT
	  
          loadingBar.style.display = "none";
          fullscreenButton.onclick = () => {
          unityInstance.SetFullscreen(1);
          };
        }).catch((message) => {
          alert(message);
        });
## Additional snippets
- Unity WebGL requires an event listener to paste from the OS clipboard. Use the following structure in script.onload.



	   // !!!
	  // !!! adding this Listener allows to copy-paste date from outside the WebGL-Build    into the WebGL-Build
        window.addEventListener('paste', function (e) {
		const str = e.clipboardData.getData('text');
		// Calls Method OnBrowserClipboardPaste in class WaxCloudWalletMainPanel while passing str as argument
           	window.unityInstance.SendMessage('WaxCloudWalletMainPanel', 'OnBrowserClipboardPaste', str);
        });
	  // !!!
       });

# Quick Start
- Create a new script inheriting from MonoBehaviour

- Add a member of type CloudWalletPlugin as well as a string to store the name of the user that is logged in.

- In the Start-method, instantiate/initialize the CloudWalletPlugin.

- Assign the EventHandlers/Callbacks allowing the CloudWalletPlugin to notify your Script about events and related Data

- Initialize the CloudWalletPlugin. This will start the communication with the Browser and create the binding between your local script and the wax-js running in the Browser.
## Usage/Examples

    private CloudWalletPlugin _cloudWalletPlugin;
    public string Account { get; private set; }

    public void Start()
    {
	// Instantiate the WaxCloudWalletPlugin
	_cloudWalletPlugin= new GameObject(nameof(CloudWalletPlugin )).   AddComponent<CloudWalletPlugin >();
	
	// Assign Event-Handlers/Callbacks
	_cloudWalletPlugin.OnLoggedIn += (loginEvent) =>
	{
		Account = loginEvent.Account;
		Debug.Log($"{loginEvent.Account} Logged In");
	};
	
	_cloudWalletPlugin.OnError += (errorEvent) =>
	{
		Debug.Log($"Error: {errorEvent.Message}");
	};
	
	_cloudWalletPlugin.OnTransactionSigned += (signEvent) =>
	{
		Debug.Log($"Transaction signed: {JsonConvert.SerializeObject(signEvent.Result)}");
	};
	
	// Inititalize the WebGl binding while passign the RPC-Endpoint of your Choice
	_cloudWalletPlugin.InitializeWebGl("https://wax.greymass.com");
	// NOTE! For other Build Targets you will need to call the related initialize Methods 
	// allowing to provide the necessary parameters needed for Mobile or Desktop-Builds
     }

    public void Login()
    {

    _cloudWalletPlugin.Login();

      }
## Images 
![](https://github.com/AzharKhemta/Gif-File-images/blob/main/Wax%20Wallet%20Unity.gif?raw=true)


## Authors

- [@MirHamzaHasan](https://github.com/MirHamzaHasan)
- [@WebSite](https://mirhamzahasan.com)


## 🔗 Links

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/company/mir-hamza-hasan/posts/?feedView=all/)
## Documentation

[Wax Wallet Sdk](https://liquiidio.gitbook.io/unity-plugin-suite/wcwunity)




## Tech Stack
**Client:** Unity  ,C#

**Plugin:** Wax Wallet Unity Sdk




## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)

