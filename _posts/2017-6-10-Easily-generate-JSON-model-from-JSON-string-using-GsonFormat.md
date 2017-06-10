---
layout: post
title: Easily generate JSON model from JSON string using GsonFormat
img: /images/JSON.jpg
---

In this post, I will explain a very useful tool, [GsonFormat](https://github.com/zzz40500/GsonFormat), for <b>Android Studio</b>, which can convert a <b>JSON</b> string to a Java class. 

Almost every software needs to communicate with a remote computer and get/post info between them. When 
exchanging data, the data can be transformed into a text. <b>JSON</b> is text, and we can convert any <b>JavaScript</b> object into JSON, and send JSON to the remote computer (I will call it "server" from now on). We can also convert any JSON received from the server into JavaScript objects. This way we can work with the data as JavaScript objects, with no complicated parsing and translations.

Creating the classes from JSON strings can be really annoying especially if the JSON data includes nested arrays and objects. Instead of trying to do this, we can use [GsonFormat](https://github.com/zzz40500/GsonFormat) and it automatically creates the Java classes for us.

## Installing GsonFormat

GsonFormat is a plugin that can be easily installed to Android Studio. 

- Using IDE built-in plugin system on <b>Windows</b>:
  - <b>File</b> > <b>Settings</b> > <b>Plugins</b> > <b>Browse repositories...</b> > <b>Search for "GsonFormat"</b> > <b>Install Plugin</b>

<br>
- Using IDE built-in plugin system on <b>MacOs</b>:
  - <b>Preferences</b> > <b>Settings</b> > <b>Plugins</b> > <b>Browse repositories...</b> > <b>Search for "GsonFormat"</b> > <b>Install Plugin</b>

<br>
- Manually:
  - Download the [latest release](https://github.com/zzz40500/GsonFormat/releases/latest) and install it manually using <b>Preferences</b> > <b>Plugins</b> > <b>Install plugin from disk...</b>
  - From official jetbrains store from [download](https://plugins.jetbrains.com/plugin/7654?pr=androidstudio)

Don't forget to restart IDE.

## Usage

I used the below JSON string for example.

~~~java
{"menu": {
  "id": "file",
  "value": "File",
  "popup": {
    "menuitem": [
      {"value": "New", "onclick": "CreateNewDoc()"},
      {"value": "Open", "onclick": "OpenDoc()"},
      {"value": "Close", "onclick": "CloseDoc()"}
    ]
  }
}}
~~~
<br>
After installation, just go to <b>Code</b> > <b>Generate</b> > <b>GsonFormat</b>

![]({{ site.baseurl }}/images/gsonformat-1.png)

<br>
A text panel will be prompt to us. Paste your <b>JSON string</b> here and press <b>Format</b> button. And lastly, press <b>OK</b> button.

![]({{ site.baseurl }}/images/gsonformat-2.png)

<br>
When you pressed <b>OK</b>, it will show you the variables and their types. You can change them from this window if you want. After that, you can again press <b>OK</b> button and finish.

![]({{ site.baseurl }}/images/gsonformat-3.png)

<br>
Thats all! It creates the class variables, methods and everything itself.  

<br>
And this is the result:

~~~java
public static class MenuBean {

    private String id;
    private String value;
    private PopupBean popup;

    public String getİd() { return id; }

    public void setİd(String id) { this.id = id; }

    public String getValue() { return value; }

    public void setValue(String value) { this.value = value; }

    public PopupBean getPopup() { return popup; }

    public void setPopup(PopupBean popup) { this.popup = popup; }

    public static class PopupBean {
        private List<MenuitemBean> menuitem;

        public List<MenuitemBean> getMenuitem() { return menuitem; }

        public void setMenuitem(List<MenuitemBean> menuitem) { this.menuitem = menuitem; }

        public static class MenuitemBean {

            private String value;
            private String onclick;

            public String getValue() { return value; }

            public void setValue(String value) { this.value = value; }

            public String getOnclick() { return onclick; }

            public void setOnclick(String onclick) { this.onclick = onclick; }
        }
    }
    }
~~~

<br>
## Conclusion

Converting JSON strings to JSON classes is a time consuming task. Creating the appropriate classes can be annoying. With [GsonFormat](https://github.com/zzz40500/GsonFormat), we don't have to do it anymore. Every Android developer should use this awesome tool.






