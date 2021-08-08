# Python-PyQt5学习笔记

## 模块

| 模块              | 功能                                                         |
| ----------------- | ------------------------------------------------------------ |
| `QtCore`          | 涵盖包核心的非GUI功能。<br>被用于处理程序中涉及到的time、文件、目录、数据类型、文本流、链接、mime、线程或进程等对象。 |
| `QtGui`           | 涵盖多种基本图形功能的类。<br>包括但不限于：窗口集、事件处理、2D图形、基本的图像和界面 和字体文本。 |
| `QtWidgets`       | 包含了一整套UI元素组件，用于建立符合系统风格的classic界面，非常方便。 |
| `QtMultimedia`    | 包含了一套类库，该类库被用于处理多媒体事件，通过调用API接口访问摄像头、语音设备、收发消息等。 |
| `QtBluetooth`     | 包含了处理蓝牙活动的类库，他的功能包括：扫描设备、连接、交互等行为。 |
| `QtNetwork`       | 包含了用于网络编程的类库，这组类程序通过提供便捷的TCP/IP 及 UDP 的 c/s 程式码集合，使得基于Qt的网络编程更容易。 |
| `QtPositioning`   | 用于获取位置信息，此模块允许使用多种方式达成定位，包括但不限于：卫星、无线网、文字信息。此应用一般用于网络地图定位系统。 |
| `Enginio`         | 用于构建客户端的应用程式库，用于在运行时访问 **Qt Cloud** 服务器托管的应用程序。 |
| `QtWebSockets`    | 包含了一组类程序，用以实现websocket协议。                    |
| `QtWebKit`        | 包含了用于实现基于webkit2的网络浏览器的类库。                |
| `QtWebKitWidgets` | 包含用于基于WebKit1的Web浏览器实现的类，用于基于QtWidgets的应用程序。 |
| `QtXml`           | 包含了用于处理XML的类库，此模块为SAX和DOM API 的实现提供了方法。 |
| `QtSvg`           | 通过一组类，为显示矢量图形文件的内容提供了方法。             |
| `QtSql`           | 提供了数据库对象的接口以供使用                               |
| `QtTest`          | 包含了可以通过单元测试，以调试PyQt5应用程式的功能。          |

<table>
<thead>
<tr>
<th style="text-align:center">模块名</th>
<th style="text-align:left">功能</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:center">Enginio</td>
<td style="text-align:left">用于访问Qt云服务的类(不推荐)</td>
</tr>
<tr>
<td style="text-align:center">QAxContainer</td>
<td style="text-align:left">访问ActiveX控件和COM对象的类</td>
</tr>
<tr>
<td style="text-align:center">Qt</td>
<td style="text-align:left">其他模块的合并</td>
</tr>
<tr>
<td style="text-align:center">Qt3DAnimation</td>
<td style="text-align:left">在模拟中支持动画的类</td>
</tr>
<tr>
<td style="text-align:center">Qt3DCore</td>
<td style="text-align:left">支持近实时仿真系统的核心类</td>
</tr>
<tr>
<td style="text-align:center">Qt3DExtras</td>
<td style="text-align:left">预先构建的元素，与Qt3D一起使用</td>
</tr>
<tr>
<td style="text-align:center">Qt3DInput</td>
<td style="text-align:left">处理使用Qt3D时用户输入的类</td>
</tr>
<tr>
<td style="text-align:center">Qt3DLogic</td>
<td style="text-align:left">启用帧同步的类</td>
</tr>
<tr>
<td style="text-align:center">Qt3DRender</td>
<td style="text-align:left">启用2D和3D呈现的类</td>
</tr>
<tr>
<td style="text-align:center">QtAndroidExtras</td>
<td style="text-align:left">特定于Android的附加类</td>
</tr>
<tr>
<td style="text-align:center">QtBluetooth</td>
<td style="text-align:left">支持设备之间蓝牙连接的类</td>
</tr>
<tr>
<td style="text-align:center">QtChart</td>
<td style="text-align:left">支持2D图表创建的类</td>
</tr>
<tr>
<td style="text-align:center">QtCore</td>
<td style="text-align:left">Qt核心类</td>
</tr>
<tr>
<td style="text-align:center">QtDBus</td>
<td style="text-align:left">使用D-Bus协议支持IPC的类</td>
</tr>
<tr>
<td style="text-align:center">QtDataVisualization</td>
<td style="text-align:left">支持3D数据可视化的类</td>
</tr>
<tr>
<td style="text-align:center">QtDesigner</td>
<td style="text-align:left">允许使用Python扩展Qt设计器的类</td>
</tr>
<tr>
<td style="text-align:center">QtGui</td>
<td style="text-align:left">widget和OpenGL gui共有的核心类</td>
</tr>
<tr>
<td style="text-align:center">QtHelp</td>
<td style="text-align:left">用于创建和查看可搜索文档的类</td>
</tr>
<tr>
<td style="text-align:center">QtLocation</td>
<td style="text-align:left">用于创建映射应用程序的类</td>
</tr>
<tr>
<td style="text-align:center">QtMacExtras</td>
<td style="text-align:left">特定于macOS和iOS的附加类</td>
</tr>
<tr>
<td style="text-align:center">QtMultimedia</td>
<td style="text-align:left">多媒体内容、摄像机和收音机的类</td>
</tr>
<tr>
<td style="text-align:center">QtMultimediaWidgets</td>
<td style="text-align:left">提供附加的多媒体相关小部件和控件的类</td>
</tr>
<tr>
<td style="text-align:center">QtNetwork</td>
<td style="text-align:left">核心网络类</td>
</tr>
<tr>
<td style="text-align:center">QtNetworkAuth</td>
<td style="text-align:left">网络授权类</td>
</tr>
<tr>
<td style="text-align:center">QtNfc</td>
<td style="text-align:left">支持设备之间NFC连接的类</td>
</tr>
<tr>
<td style="text-align:center">QtOpenGL</td>
<td style="text-align:left">在传统窗口小部件中呈现OpenGL的类(不推荐)</td>
</tr>
<tr>
<td style="text-align:center">QtPositioning</td>
<td style="text-align:left">从卫星、wifi等获取定位信息的类</td>
</tr>
<tr>
<td style="text-align:center">QtPrintSupport</td>
<td style="text-align:left">实现打印的类</td>
</tr>
<tr>
<td style="text-align:center">QtPurchasing</td>
<td style="text-align:left">支持从应用商店购买应用程序的类</td>
</tr>
<tr>
<td style="text-align:center">QtQml</td>
<td style="text-align:left">与QML语言集成的类</td>
</tr>
<tr>
<td style="text-align:center">QtQuick</td>
<td style="text-align:left">使用Python代码扩展QML应用程序的类</td>
</tr>
<tr>
<td style="text-align:center">QtQuickWidgets</td>
<td style="text-align:left">用于在传统小部件中呈现QML场景的类</td>
</tr>
<tr>
<td style="text-align:center">QtRemoteObjects</td>
<td style="text-align:left">用于在进程或系统之间共享QObject的API的类</td>
</tr>
<tr>
<td style="text-align:center">QtSensors</td>
<td style="text-align:left">用于访问系统硬件传感器的类</td>
</tr>
<tr>
<td style="text-align:center">QtSerialPort</td>
<td style="text-align:left">用于访问系统的串行端口的类</td>
</tr>
<tr>
<td style="text-align:center">QtSql</td>
<td style="text-align:left">与SQL数据库集成的类</td>
</tr>
<tr>
<td style="text-align:center">QtSvg</td>
<td style="text-align:left">提供对SVG支持的类</td>
</tr>
<tr>
<td style="text-align:center">QtTest</td>
<td style="text-align:left">支持GUI应用程序单元测试的类</td>
</tr>
<tr>
<td style="text-align:center">QtWebChannel</td>
<td style="text-align:left">用于Python和HTML/JavaScript之间的点对点通信的类</td>
</tr>
<tr>
<td style="text-align:center">QtWebEngine</td>
<td style="text-align:left">用于将QML Web引擎对象与Python集成的类</td>
</tr>
<tr>
<td style="text-align:center">QtWebEngineCore</td>
<td style="text-align:left">Web引擎核心类</td>
</tr>
<tr>
<td style="text-align:center">QtWebEngineWidgets</td>
<td style="text-align:left">基于Chromium的web浏览器</td>
</tr>
<tr>
<td style="text-align:center">QtWebKit</td>
<td style="text-align:left">基于WebKit2的web浏览器(已弃用)</td>
</tr>
<tr>
<td style="text-align:center">QtWebKitWidgets</td>
<td style="text-align:left">基于WebKit1的web浏览器(已弃用)</td>
</tr>
<tr>
<td style="text-align:center">QtWebSockets</td>
<td style="text-align:left">实现WebSocket协议的类</td>
</tr>
<tr>
<td style="text-align:center">QtWidgets</td>
<td style="text-align:left">用于创建经典桌面样式ui的类</td>
</tr>
<tr>
<td style="text-align:center">QtWinExtras</td>
<td style="text-align:left">特定于Windows的附加类</td>
</tr>
<tr>
<td style="text-align:center">QtX11Extras</td>
<td style="text-align:left">特定于X11的其他类</td>
</tr>
<tr>
<td style="text-align:center">QtXml</td>
<td style="text-align:left">支持SAX和DOM到XML接口的类</td>
</tr>
<tr>
<td style="text-align:center">QtXmlPatterns</td>
<td style="text-align:left">支持其他XML技术的类</td>
</tr>
<tr>
<td style="text-align:center">sip</td>
<td style="text-align:left">绑定开发人员和用户的实用程序</td>
</tr>
<tr>
<td style="text-align:center">uic</td>
<td style="text-align:left">用于处理Qt设计器创建的文件的类</td>
</tr>
</tbody>
</table>