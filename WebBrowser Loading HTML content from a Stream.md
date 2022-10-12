# See:
- [Loading HTML content from a Stream](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752047(v=vs.85)?redirectedfrom=MSDN)
- [Loading HTML content from a Stream](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752047(v=vs.85)?redirectedfrom=MSDN)
- [WebBrowser Control](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752040(v=vs.85))
- [WebBrowser Control Overviews and Tutorials](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752041(v=vs.85))

# See2:
- [WebBrowser, IPersistStreamInit and javascript](https://stackoverflow.com/questions/3443667/webbrowser-ipersiststreaminit-and-javascript)
- [Which is the best way to load a string (HTML code) in TWebBrowser?](https://stackoverflow.com/questions/39773033/which-is-the-best-way-to-load-a-string-html-code-in-twebbrowser)
- [ How to load an HTML document from a stream into a TCppWebBrowser. ](https://edn.embarcadero.com/article/26729)
- [Load HTML source code](https://stackoverflow.com/questions/17137506/load-html-source-code)
- [Load TWebBrowser's document content from stream or string](https://www.yourdelphi.com/topic_523156_a39d.htm)

#  LoadBlankDoc(WB: TWebBrowser);
- Test is Ok, with delphi 7  in windows xp sp3

```
procedure LoadBlankDoc(WB: TWebBrowser);
begin
 WB.Navigate('about:blank', EmptyParam, EmptyParam, EmptyParam, EmptyParam);
 while WB.ReadyState <> READYSTATE_COMPLETE do
 begin
  Application.ProcessMessages;
  Sleep(0);
 end;
end;
```
- 
