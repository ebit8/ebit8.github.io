---
{"dg-publish":true,"permalink":"/10_Blog/raspberry pi 5でGodotゲームを動かすとテキスト更新で描画不具合/","created":"2026-04-04T16:42:02.657+09:00","updated":"2026-04-12T12:30:12.208+09:00"}
---

---
### 環境
Godot v4.6.2.stable.mono - Windows 11 (build 26200) - Multi-window, 2 monitors - OpenGL 3 (Compatibility) - NVIDIA GeForce RTX 5070 Ti (NVIDIA; 32.0.15.9186) - AMD Ryzen 9 5950X 16-Core Processor (32 threads) - 63.92 GiB memory

Raspberry pi 5 4GB

### 不具合と解決方法
起動直後はLabelが正常に表示されるが、Label.Textを更新した際に、下図のように文字の一部がレンダリングされなくなる（横長の帯状）症状が発生。
![Pasted image 20260412014807.png](/img/user/_config/Extra/Pasted%20image%2020260412014807.png)
※元は時刻を表示しており、「HH:MM:SS」


原因としては、プロジェクト設定のレンダリングメソッドがmobileだったため。gl_compatibilityに修正してビルドすると、Textを更新しても症状は発生しなかった。
![Pasted image 20260412014130.png](/img/user/_config/Extra/Pasted%20image%2020260412014130.png)

![Pasted image 20260412014350.png](/img/user/_config/Extra/Pasted%20image%2020260412014350.png)

### 補足
レンダリングメソッドをgl_compatibilityにしたビルドをラズパイ側で動かした際に以下のエラーが出る。動かすうえで支障は無さそうなので放置しているが、たぶんちゃんと対応した方がいい。

```
WARNING: Your video card drivers seem not to support the required OpenGL version, switching to OpenGLES.
```

たぶんここのドライバー.linuxbsdをopengl3_esにすればいいのかな？グラフィックAPIに関しては詳しくないのでわからんけど...
![Pasted image 20260412122404.png](/img/user/_config/Extra/Pasted%20image%2020260412122404.png)