<a name="top"></a>

<p align="center"> 
  <a href="https://www.linkedin.com/in/clarence-fong" target="_blank">
    <img width="50" height="50" alt="LinkedIn" src="https://github.com/user-attachments/assets/7ab6e12b-ca8a-4aa6-8f10-79ba89d485b5" />
  </a>
  <a href="mailto:abc1230940@gmail.com">
    <img width="50" height="50" alt="Gmail" src="https://github.com/user-attachments/assets/4e0491ce-239c-413c-b433-74a5ff48f231" />
  </a>
  <a href="https://www.instagram.com/cyberbrexel?igsh=MXNxeWJid2VxZWxxaw%3D%3D&utm_source=qr" target="_blank">
    <img width="50" height="50" alt="Instagram Old" src="https://github.com/user-attachments/assets/62e4672b-d424-4489-a204-c301040905a3" />
  </a>
  <a href="https://discordapp.com/users/cyberbrexel" target="_blank">
    <img width="50" height="50" alt="Discord" src="https://github.com/user-attachments/assets/f76173ca-fad3-4390-bca1-5c2305bc748e" />
  </a>
  <a href="https://www.reddit.com/user/abc1230940/" target="_blank">
    <img width="50" height="50" alt="Reddit" src="https://github.com/user-attachments/assets/6e9bd985-dfa3-4349-b966-4cf49362bd61" />
  </a>
</p> <br>


<h2 align="center"> CyberDefenders Write-up - BlackEnergy </h2>
<h2 id="scenario"> Scenario </h2>
<p> A multinational corporation has suffered a cyber attack, resulting in the theft of sensitive data. The attack employed a previously unseen variant of the BlackEnergy v2 malware. The company's security team has obtained a memory dump from the infected machine and is seeking your expertise as a SOC analyst to analyze the dump in order to understand the scope and impact of the attack.</p>
<p align="right">(<a href="#top">Back to Top</a>)</p>


<h2 id="tools-used"> Tools Used </h2>
<ol>
  <li> <a href="https://github.com/volatilityfoundation/volatility/releases"> Volatility 2 </a> </li>
  <li> <a href="https://blog.onfvp.com/post/volatility-cheatsheet/"> Volatility 3 CheatSheet </a> </li>
</ol>
<h3> Installation of Volatility 2 </h3>
<p> Step 1: Download Volatility 2 Standalone Executable </p> 
<img width="1132" height="439" alt="Screenshot 2026-06-19 194047" src="https://github.com/user-attachments/assets/aa27fa48-6446-4c72-b9ec-ecb1ce12e8d8" />
<p> Download the Volatility 2 standalone executable from the <a href="https://github.com/volatilityfoundation/volatility/releases"> offical GitHub repository. </a> </p>
<p> Step 2: Verify Installation </p>
<pre> <code lang="cmd"> cd path\\to\\volatility-2.6 </code> </pre>
<pre> <code lang="cmd"> .\volatility_2.6_win64_standalone.exe -h </code> </pre>
<img width="871" height="700" alt="image" src="https://github.com/user-attachments/assets/fcd6b93b-e627-44dc-bdfa-e0e96c6004e1" />
<p> The help menu will be shown if the installation is successful. Plugins can also be found in the help menu for memory analysis. </p>
<p align="right">(<a href="#top">Back to Top</a>)</p>


<h2 id="questions"> Questions </h2>
<p> <strong> 1. Which volatility profile would be best for this machine? </strong> </p>
<p> This is the very first thing to do when analyzing the memory dump with Volatility 2. After finding the profile of the investigated machine, volatility 2 can analyze the data from the memory dump with this profile. </p>
<pre> <code lang="cmd"> volatility_2.6_win64_standalone.exe -f "path\\to\\CYBERDEF-567078-20230213-171333.raw" imageinfo </code> </pre>
<img width="1238" height="257" alt="Screenshot 2026-06-19 170244" src="https://github.com/user-attachments/assets/bfb6549d-d31e-4a5f-9bdb-8bfe9d548e0f" />
<p> the suggested profiles were WinXPSP2x86 and WinXPSP3x86 but the best for the machine was <strong>WinXPSP2x86 </strong>. </p>
<br>
<p> <strong> 2. How many processes were running when the image was acquired? </strong> </p>
<p> To find all processes running in the memory captured, we used the plugin pslist. </p>
<pre> <code lang="cmd"> volatility_2.6_win64_standalone.exe -f "path\\to\\CYBERDEF-567078-20230213-171333.raw" pslist </code> </pre>
<img width="1387" height="480" alt="Screenshot 2026-06-19 171323" src="https://github.com/user-attachments/assets/66d5aca5-e416-4175-852c-754dbe3ab656" />
<p> There were total 25 processes running in the memory. However 6 of them exited, indicating that those processes terminated. Therefore, 25 - 6 = <strong>19 </strong>were running in the memory when captured.</p>
<p align="right">(<a href="#top">Back to Top</a>)</p>
