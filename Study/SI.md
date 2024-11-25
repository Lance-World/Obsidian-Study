
### What influence the SI?

1. 時脈分佈: 不良的時脈分佈可能導致時序錯誤。
2. 訊號路徑設計 [[Return Paths]] [[Ground bounce]]
3. 殘樁問題 :未移除的信號 stub 導致反射。
4. 雜訊容限 : 雜訊超出容限時，可能發生錯誤。
5. 阻抗匹配和負載 [[Target impedance]]
6. 傳輸線效應: 反射[[Reflection coefficient]]、延遲、損耗[[Insertion Loss]]
7. 訊號路徑回流電流 [[Return Paths]]
8. 終端 [[terminal-end]] :終端電阻不足會引起反射。
9. 去耦 [[Decoupling Capacitor]]
10. 電源分佈 電壓波動影響訊號質量。

 ---

### Three Core Aspects of Signal Integrity:

1. 時序 ( Timing )：信號的傳遞是否準時，避免延遲和失序。
2. 雜訊 ( Noise ):  Ringing, [[Crosstalk]], [[Power rail collapse]] 等問題
3. 電磁干擾 ( Electromagnetic interference - EM)：電磁輻射對信號的干擾。

---
### Influence SI

![[Influence SI.png]]

---
### Signal Transmission 基礎

> [[Bandwidth]] : 
> 信號的等效頻寬，用於估算數字信號傳輸所需的頻率範圍

 >[[Voltage Formula]] - 電阻,電感,電容
 >  1. $$V=IR$$
 >  2. $$V={L}\frac{dI}{dt}$$
 >  3. $$I_C=C\frac{dV}{dt}$$

>[[Skin effect]] : 高頻電流集中於導體表面，增加損耗。

---
### [[Return Paths]] Design:
| **Return Path** | **描述**                        | **特性**                                                             |
| --------------- | ----------------------------- | ------------------------------------------------------------------ |
| **高頻信號的回流行為**   | 高頻電流經由低阻抗路徑（電容）回流，避免經過主要直流電阻  | - **多層 PCB 結構**可提供有效回路                                             |
| **位移電流的貢獻**     | 隨電場變化產生的虛擬電流，在高頻條件下對電場擾動有顯著影響 | - 位移電流公式：![[Displacement current 1.png]]<br>- 幫助高頻信號回流，減少接地反彈和 EMI |
| **回流設計優化**      | 通過**接地層或電源層間電容**形成低阻抗回流路徑     | - 提高電源完整性 (PI)  <br>- 減少接地電壓波動                                     |

---
### Transmission line Effects

Key Effects
1.  Reflections from the Capacitance End Terminations

    >[[Capacitance impedance]]:
    >$$Z_c(t)=\frac{V}{I}\frac{V}{C\frac{dV}{dt}}$$
    >[[Reflection coefficient]]:  
    >$$\rho(t)=\frac{Z_C-Z_0}{Z_C+Z_0}$$

---

### [[Losses in Transmission lines]]

| **能量損失類型**                         | **描述**                                                      |
| ---------------------------------- | ----------------------------------------------------------- |
| **輻射造成的能量損失 (Radiated Losses)**    | 電磁輻射會將部分能量散失到周圍環境，特別是在高頻訊號下，導致信號能量的減少。                      |
| **與鄰近導線耦合 (Crosstalk Coupling)**   | 鄰近導線之間的耦合會引起串擾，將部分能量耦合到其他線路上，造成信號衰減與干擾。                     |
| **阻抗不匹配 (Impedance Mismatch)**     | 當傳輸線的特性阻抗與負載阻抗不匹配時，會導致部分**信號反射**，減少了有效能量的傳輸。                |
| **導體電阻造成的能量損失 (Conductor Losses)** | 傳輸線的導體材料具有一定的電阻，尤其在**長距離傳輸**時，會導致訊號的直流與高頻損耗。                |
| **介電質造成的能量損失 (Dielectric Losses)** | **介電質吸收能量**，特別在**高頻**下，介電損耗會顯著降低信號強度，且絕緣性不佳時會產生漏電流，進一步消耗能量。 |

---

### [[Dielectric Losses]]：

- ##### [[Df and Dk]] : Dk 穩定性保證信號速度一致，Df 小則減少信號損失。

>1. **Dissipation Factor (Df)**：
  >$$D_f=tan(\delta), v=\frac{c}{\sqrt{D_k}}$$
	- **介電質結構與電偶拘束**：當**電偶被聚合物緊密拘束**時，能量耗散減少，**Df 值低**。
    - **頻率**：隨**頻率增加**，電偶振動加劇，能量損耗增大，**Df 值上升**。
    >**電容電流 (Ic)**：由於絕緣材料具有電容特性，會產生一種與電壓相位差 90° 的電流。 
    >**漏洩電流 ([[Ir]])**：由於絕緣材料的微小導電性，會產生一種與電壓同相的電流。

>2. **DK值**的穩定是電路板可靠性的保證，**DF值**應盡可能小以減少信號損失
>![[tan(delta).png]]

---
- ## [[Differential pair]]
#具有良好的自我EMC特性，因為其對稱的正負信號能相互抵消，降低對外輻射。然而，若存在共模信號，會增加對外的EMI，導致電磁干擾。
	為減少共模影響，應保持導線對稱、匹配良好，並加入共模濾波。

- #### [[Common Signal]]
共模信號會導致兩條傳輸線上的電磁場疊加，增加對外界的干擾。

- **噪聲抑制**： 共模訊號的抗噪聲能力較差
	1. 確保導線對稱、間距均勻。
	2. 減少共模來源，如電源雜訊、阻抗不匹配。
	3. 加入適當的共模濾波設計，降低共模訊號影響。-
    
- **用途**： 
  >共模訊號通常在一些較簡單的系統中使用，特別是當系統不要求強大的抗干擾能力或在測量共模噪聲時會用到。
    
- **優點**：
    - 設計簡單，成本較低。
    - 在簡單的信號應用中，對於訊號的傳輸不會有太多要求。
- **應用範疇**： 
  適用於較低頻率或較短距離的信號傳遞，通常是簡單的信號傳輸，或者當我們只關心共模噪聲而非信號本身時。
  
---

- #### [[Differential signalling]]
  #是由differential_signal看到的阻抗
強調信號之間的差異，能有效地抑制外來噪聲，適合用於高速和高頻的數據傳輸。

- **噪聲抑制**： 差動信號具有強大的抗干擾能力。因為外部噪聲會同時影響兩條線，但由於接收端僅關注兩條線之間的電壓差，當兩條線上的噪聲是相同的時，這些噪聲會被抵消。

- **用途**： 常見於需要高速傳輸和長距離傳輸的應用中。比如 USB、Ethernet、HDMI、Serial通信等。

- **優點**：
    - 抗干擾能力強，適合在噪聲較多的環境中使用。
    - 可以有效減少信號在長距離傳輸中的衰減和失真。
- **應用範疇**： 
	  適用於數據密集型、高頻信號傳輸，如數據通訊、電源線抑制等。

---

- #### [[Differential impedance]]:
#是由differential_signal看到的阻抗

![[Differential pair.png]]


- $$Z_0=\frac{V_{one}}{I_{one}}$$
-  $$Z_{diff}=\frac{V_{diff}}{I_{one}}=\frac{2\times V_{one}}{I_{one}}=2Z_0$$

- #### Even-mode vs. Odd-mode impedance
#依照不同的mode驅動，在單條線的訊號看到的阻抗

---
- #### [[Signalling mode]]
  
  - **信號模式分為兩類**：
    - **Differential Signal（差動信號）**：傳遞兩條線之間的差異。
    - **Common Signal（共模信號）**：傳遞兩條線之間相同的信號。
- **差動信號進一步細分為模態**：
    - **[[Odd Mode]]（奇模）**：兩條線的電壓大小相等、方向相反，用於差分訊號傳輸。
    - **[[Even Mode]]（偶模）**：兩條線的電壓大小相等、方向相同，多出現在共模噪聲中。
- **阻抗相關性**：
    - **Differential Impedance（差模阻抗）**：描述兩條信號線之間的阻抗，對信號的完整性影響較大。
    - **Common Impedance（共模阻抗）**：描述兩條線對地之間的阻抗，主要用於評估共模噪聲的影響。
    
![[Signal mode.png]]

---
#### [[Eye Diagram]]

- 觀察**時脈驅動匯流排** (串列訊號) 上訊號完整性的一種方法。
---
#### Equalization:
預先降低訊號低頻部分傳遞訊號，經傳輸線衰減高頻部分厚，高頻與低頻部分已被"等化"，因此波形維持完整。

#### De-emphasis:
PCIe 1.0和PCIe 2.0使用的物理介質是普遍的FR4 PCB板材和廉價的接插件，為保證在該介質上的有效信號傳輸，PCI-SIG協會使用了8b/10b編碼和發送端的固定參數的去加重(De-emphasis)均衡，其過程無需進行均衡參數協商。

1. 在PCIe 1.0中，去加重值是固定值-3.5dB
2. 在PCIe 2.0中，去加重值是固定值-3.5dB 和 -6dB，無法動態調整

>[[Link Equalization-PCIE]]
>鏈路均衡通過 PCIe 規範中定義的preset值來實現，preset 指不同的預過沖(Preshoot)和去加重(De-emphasis) 的組合。

(https://www.graniteriverlabs.com/zh-tw/technical-blog/pcie-dynamic-link-equalization)
![[鏈路均衡PCIE.png]]


---

### SerDes
(https://yrgnthu.medium.com/%E6%B7%BA%E8%AB%87%E9%80%9A%E8%A8%8A%E7%B3%BB%E7%B5%B1%E4%B8%AD%E7%9A%84%E7%AD%89%E5%8C%96%E5%99%A8-45ab8b0029c9)


序列器（Serializer）和解序列器（Deserializer）合稱SerDes的電路

![[Normal SerDes system.png]]
