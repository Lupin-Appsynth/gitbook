---
description: "\U0001F914 อยากใช้ Windows กับ Linux พร้อมกันทำไง"
---

# 🔄 WSL

## 🤠 รู้ป่ะ ?

โดยปรกติโปรแกรมต่างๆนั้นจะมีต้นกำเหนิดมาจาก **Linux OS** ซะส่วนใหญ่ไม่ว่าจะเป็น [MongoDB](https://www.mongodb.com/), [Nginx](https://www.nginx.com/), [Redis](https://redis.io/), [Anaconda ](https://www.anaconda.com/)บลาๆ แล้วพอเวลาผ่านไปมีคนใช้เยอะขึ้นจนดังเป็นพลุแตก แน่นอนว่าขาเดฟในฝั่ง Windows ก็เป็นกลุ่มตลาดใหญ่เช่นกัน ดังนั้นเขาก็จะทำการแปลงโปรแกรมเหล่านั้นให้ฝั่ง **Windows OS** ใช้งานได้ แต่ด้วยชาติกำเหนิดของมันที่ถูกสร้างและ Optimize มาจาก Linux ทำให้บางเรื่องก็ยังไม่สามารถดึงประสิทธิภาพออกมาได้เต็ม 100% และความสามารถบางอย่างก็ยังใช้งานได้แค่ฝั่ง Linux เท่านั้น เพราะความสามารถบางตัวไม่มีบน Windows หรือยังแปลงมาไม่เสร็จ

![](../../.gitbook/assets/image%20%281222%29.png)

## 🤯 WSL

จากที่เล่ามาทาง Microsoft ก็รู้จุดอ่อนนี้เหมือนกันเลยทำให้เกิดไอเดียว่า **จะดีกว่าไหมถ้า Windows ทำงานร่วมกับ Linux ได้เป็นหนึ่งเดียวกันเลย?** ดังนั้นเลยเกิดโปรเจคที่ชื่อว่า **Windows Subsystem for Linux** หรือ **WSL** เกิดขึ้น ซึ่งมันจะทำให้**เราสามารถใช้งาน Linux บน Windows ได้แบบ Native** โดยที่ไม่ต้องลง Virtual Machine หรือ Hyper-V ใดๆเลย 😘

![](../../.gitbook/assets/image%20%281224%29.png)

ดังนั้นถ้าเราใช้ WSL มันจะทำให้เครื่องของเราใช้ Linux ได้แบบ Native แถมยังเลือกใช้ Linux ได้หลายตัวพร้อมๆกันด้วย ตามรูปด้านล่าง

![](../../.gitbook/assets/image%20%281215%29.png)

![](../../.gitbook/assets/image%20%281218%29.png)

แถมยังแชร์ไฟล์/ไดรฟ์ ได้แบบเป็นหนึ่งเดียวกัน ไม่ต้องคอยแปลง format หรือจัดการเรื่อง network อะไรด้วย

![](../../.gitbook/assets/image%20%281227%29.png)

![](../../.gitbook/assets/image%20%281221%29.png)

และความแจ่มแมวอีกอย่างคือ เราสามารถใช้ WSL ควบคู่กับ 🐳 **Docker** ได้ด้วยนะจ๊ะ

![](../../.gitbook/assets/image%20%281225%29.png)

## 🛠️ Installation

ถ้าใครอ่านมาถึงตรงนี้ **ดชแมวน้ำ** ก็น่าจะขายของได้แล้วล่ะ ดังนั้นมาเตรียมติดตั้ง WSL กันดีกั่ว ตามขั้นตอนพวกนี้

### 🔥 Requirements

อย่างแรกเลยคือตัว Windows ของเราจะต้องเป็นเวอร์ชั่นที่รองรับก่อนตามตารางด้านล่าง

| System | Version |
| :--- | :--- |
| x64 | ขั้นต่ำ  **Version 1903** **Build 18362** |
| ARM64 | ขั้นต่ำ  **Version 2004** **Build 19041** |

ส่วนวิธีตรวจว่าเครื่องตัวเองรองรับหรือเปล่าให้กดปุ่ม **Windows** แล้วพิมพ์คำว่า **`winver`** แล้วกด enter ก็จะเจอเวอร์ชั่นของเครื่องเรา แล้วก็เอามาเช็คกับตารางตัวนี้เอาครับ ส่วนเครื่องใครยังไม่ใช่เวอร์ชั่นที่รองรับก็รบกวนกดที่ลิงค์นี้  [**Update Windows version**](ms-settings:windowsupdate) เพื่อไปทำการอัพเกรดเป็นตัวล่าสุดก่อนละกัน

### 🔥 Enable WSL

ต่อมาก็จะเปิดให้เครื่องเราสามารถใช้ WSL ได้ โดยการเปิด **`PowerShell`** ขึ้นมาในโหมด admin ซึ่งสามารถทำได้โดยกดปุ่ม Windows แล้วพิมพ์ว่า `powershell` แล้วเราจะเห็นโปรแกรม PowerShell โชว์ขึ้นมา ให้ทำการคลิกขวาแล้วเลือกเป็น `Run as administrator` แล้วตอบ yes ได้เบย 

![](../../.gitbook/assets/image%20%281219%29.png)

พอหน้าจอดำๆเปิดขึ้นมาละก็ copy คำสั่งด้านล่างลงไป แล้วกด enter โลด

```bash
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

ถัดมาก็ทำการเปิด Virtual Machine feature โดยการใช้คำสั่งด้านล่าง

```bash
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

ถึงตรงนี้ หากเครื่องใครใช้ WSL เวอร์ชั่น 1 อยู่ อาจจะต้อง Restart เครื่องซักรอบนึงนะ ส่วนใครอยากจะย้ำให้มั่นใจก็ restart ด้วยกะได้

### 🔥 Install Linux kernel

ถัดมาเราก็จะติดตั้ง **Linux kernel** ให้กับเครื่องเรา โดยการดาวโหลดไฟล์ด้านล่างมาติดตั้งให้เรียบร้อย \(เลือกติดตั้งแค่ตัวเดียวนะขึ้นอยู่กับว่าเครื่องเราเป็น x64 หรือ ARM\) 

> ตอนติดตั้งมันกดแค่ 2-3 ทีก็ติดตั้งเสร็จละ ไวมากไม่ต้องตกใจนะ 😂

* \*\*\*\*[**x64 system Linux kernel**](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)\*\*\*\*
* \*\*\*\*[**ARM64 system Linux kernel**](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_arm64.msi)\*\*\*\*

{% hint style="warning" %}
**หมายเหตุ**  
สำหรับใครที่ไม่รู้ว่าเครื่องตัวเองเป็น x64 หรือ ARM64 สามารถตรวจง่ายๆโดยใช้คำสั่งด้านล่างนี้ครับ

```text
systeminfo | find "System Type"
```
{% endhint %}

{% hint style="warning" %}
**หมายเหตุ**  
สำหรับคนที่เคยติดตั้ง WSL เวอร์ชั่นเก่าแล้วอยากเปลี่ยนมาใช้เวอร์ชั่นล่าสุด \(ณ ตอนที่เขียนบทความนี้คือเวอร์ชั่น 2\) ก็สามารถทำได้ง่ายๆโดยใช้คำสั่งด้านล่างนี้ครัช

```text
wsl --set-default-version 2
```
{% endhint %}

### 🔥 Install Linux distribution

จากตรงนี้เครื่องเราก็จะพร้อมทำงานทุกอย่างละ สุดท้ายเราก็ต้องเลือกว่าจะใช้ Linux ตัวไหนบ้าง โดยเพื่อนๆสามารถเลือกได้จากลิสค์ด้านล่างนี้เลยกั๊ฟ

* [Ubuntu 16.04 LTS](https://www.microsoft.com/store/apps/9pjn388hp8c9)
* [Ubuntu 18.04 LTS](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q)
* [Ubuntu 20.04 LTS](https://www.microsoft.com/store/apps/9n6svws3rx71)
* [openSUSE Leap 15.1](https://www.microsoft.com/store/apps/9NJFZK00FGKV)
* [SUSE Linux Enterprise Server 12 SP5](https://www.microsoft.com/store/apps/9MZ3D1TRP8T1)
* [SUSE Linux Enterprise Server 15 SP1](https://www.microsoft.com/store/apps/9PN498VPMF3Z)
* [Kali Linux](https://www.microsoft.com/store/apps/9PKR34TNCV07)
* [Debian GNU/Linux](https://www.microsoft.com/store/apps/9MSVKQC78PK6)
* [Fedora Remix for WSL](https://www.microsoft.com/store/apps/9n6gdm4k2hnc)
* [Pengwin](https://www.microsoft.com/store/apps/9NV1GV1PXZ6P)
* [Pengwin Enterprise](https://www.microsoft.com/store/apps/9N8LP0X93VCP)
* [Alpine WSL](https://www.microsoft.com/store/apps/9p804crf0395)

### 🔥 Set up a new distribution

หลังจากที่ติดตั้ง Linux distribution เสร็จแล้ว โดยปรกติ Linux OS นั้นเราจะต้องเข้าไปตั้ง Username & Password ต่างๆก่อนถึงจะเข้าไปใช้งานได้ \(จริงๆ Mac, Windows ก็มีเรื่องพวกนี้เหมือนกัน แต่ส่วนใหญ่เราจะทำผ่าน GUI อยู่แล้วเลยไม่รู้ตัว\) ดังนั้นให้เปิด Linux ที่เราพึ่งติดตั้งขึ้นมา แล้วตั้ง username & password โลด \(สำหรับคนไม่เคยใช้ Linux ตอนใส่รหัสผ่านมันจะไม่แสดงสิ่งที่เราพิมพ์นะ ให้ใส่ให้ครบแล้วกด enter ได้เลย\)

![&#xE43;&#xE04;&#xE23;&#xE25;&#xE07;&#xE44;&#xE23;&#xE01;&#xE47;&#xE40;&#xE1B;&#xE34;&#xE14;&#xE2D;&#xE31;&#xE19;&#xE19;&#xE31;&#xE49;&#xE19;&#xE02;&#xE36;&#xE49;&#xE19;&#xE21;&#xE32; &#xE2A;&#xE48;&#xE27;&#xE19;&#xE1B;&#xE4B;&#xE21;&#xE25;&#xE07; Ubuntu &#xE01;&#xE31;&#xE1A; Debian](../../.gitbook/assets/image%20%281220%29.png)

หลังจากที่สร้าง user เสร็จแล้ว สุดท้ายก็ทำการอัพเกรด packages กันหน่อยด้วยคำสั่งด้านล่าง

```bash
sudo apt update && sudo apt upgrade
```

จากทั้งหมดที่ทำมาก็เป็นอันว่าเครื่องคอมของเรา มี Windows และ Linux ทำงานอยู่บนเครื่องเดียวกันเรียบร้อยแล้วขอรับ ฮูเร่!! 🎉

### 🔥 Install Windows Terminal

ตัวนี้ไม่จำเป็นต้องลงก็ได้ แต่ส่วนตัวแมวน้ำชอบ เพราะมันทำให้เราเปิดหลายๆ Terminal ขึ้นมาได้พร้อมๆกัน แถมยังจัดการตกแต่งสีอะไรต่างๆได้ด้วย ทำให้เราไม่ต้องสลับจอไปๆมาๆเลย ซึ่งเพื่อนๆสามารถไปดาวโหลดมาติดตั้งได้จากลิงค์นี้ครัช [Microsoft Store](https://aka.ms/terminal)

![](../../.gitbook/assets/image%20%281216%29.png)

ซึ่งหลังจากติดตั้งเสร็จแล้ว เราก็ลองเปิดขึ้นมาเล่นดูก็จะพบว่า เราสามารถเลือกที่จะเปิด Terminal มาได้ทุกรูปแบบ Command Prompt, PowerShell, CloudShell, Linux ต่างๆที่เราติดตั้งไว้ได้หมดเลย ส่วนใครที่อยากจะตกแต่งลูกเล่นเพิ่มเติมต่างๆก็สามารถกด `Setting` ไปเล่นต่อได้ โดยสามารถศึกษาได้จากลิงค์นี้กั๊ฟ [**Windows Terminal**](https://docs.microsoft.com/en-us/windows/terminal/)\*\*\*\*

![](../../.gitbook/assets/image%20%281226%29.png)

![https://docs.microsoft.com/en-us/windows/terminal/panes](../../.gitbook/assets/alt-click-pane.gif)

## 🐳 Docker

สำหรับขาเดฟที่ชื่นชอบพี่วาฬก็สามารถนำ WSL มาทำงานร่วมได้เช่นกัน โดยการคลิกขวาที่ไอคอนพี่วาฬแล้วเลือก Settings &gt; General แล้วติ๊กเลือกว่าจะทำงานกับ WSL ได้เบย

![](../../.gitbook/assets/image%20%281217%29.png)

ถัดมาเราก็จะมาตั้งค่าว่าจะให้ Linux ตัวไหนที่ใช้งาน Docker ได้บ้าง ตามรูปด้านล่าง

![](../../.gitbook/assets/image%20%281223%29.png)

หลังจากที่กดตกลงเรียบร้อย + รีสตาร์ท Docker เรียบร้อย เจ้า Linux ของเราก็จะสามารถใช้งาน docker command ได้แบ้ว แถมยังไม่ต้องใช้ Hyper-V ในการสร้าง Linux VM อีกด้วย นั่นหมายความว่าเครื่องของเรากับ Linux ทำงานแบบแชร์ Resource พวก CPU, Memory, Storage กันได้อย่างแท้จริง ไม่ต้อง dedicate ของเหล่านั้นอีกแล้ว **แปลเป็นภาษามนุษย์ง่ายๆว่า เครื่องไม่อืดนั่นเอง 😂**

![](../../.gitbook/assets/image%20%281228%29.png)

สำหรับเพื่อนๆที่ต้องการศึกษาการใช้ WSL ควบคู่กับ Docker ก็สามารถไปอ่านต่อได้จากเอกสารหลักของ Docker ได้เลยนะกั๊ฟ [**Docker Desktop WSL 2 backend**](https://docs.docker.com/docker-for-windows/wsl/) ซึ่งแทบจะเรียกว่ามันเป็น Best Practices ของเขาในการใช้งานของ Windows เลยก็ว่าได้ 😘

