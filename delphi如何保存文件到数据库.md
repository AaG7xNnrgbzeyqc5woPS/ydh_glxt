# 0. See:
  - [delphi 把文件以二进制形式存入数据库](https://www.programminghunter.com/article/16362068675/)
  - [ delphi 把文件以二进制形式存入数据库 -- 更早源... ](http://www.360doc.com/content/12/0320/15/7389824_195972415.shtml)
  - [Delphi+Mysql(如何将一个二进制文件保存到mysql数据库中？)](https://bbs.csdn.net/topics/133012)

# 1. 原文拷贝
```
//上传
procedure TForm1.BitBtn1Click(Sender: TObject);
var
  fname:string;
begin
  if not OpenDialog1.Execute then
  begin
    Exit;
  end;

  fname:=OpenDialog1.FileName;
  try
    with adoquery1 do
    begin
      Close;
      SQL.Clear;
      SQL.Add(' insert into wjtuploadtest ') ;
      SQL.Add(' (fname,bfile) ');
      SQL.Add(' values(:fname,:bfile)') ;
      Parameters.ParamByName('fname').Value:=fname;
      Parameters.ParamByName('bfile').LoadFromFile(fname,ftBlob);
      Prepared;
      ExecSQL;
    end;
  except
      ShowMessage('文件上传失败，请联系管理员');
  end;
end;
//下载
procedure TForm1.BitBtn2Click(Sender: TObject);
begin
  try
     with ADOQuery1 do
     begin
       Close;
       SQL.Clear;
       SQL.Add(' select bfile from wjtuploadtest where id= ''2'' ');
       Open;
       edit;
       TBlobField(FieldByName('bfile')).SaveToFile('c:\a56.pdf');
       Post;
     end;
  except
     ShowMessage('文件下载失败，请联系管理员');
  end;
end;
```
# 2. 如何将一个二进制文件保存到mysql数据库中？
TBlobField(Table1.FieldbyName('blob')).LoadFromFile(Filename);
......SaveToFile();

# 3. MS SQL server 可以使用存储过程，存储过程的输入和输出参数支持 image格式，也就是二进制
```
```

