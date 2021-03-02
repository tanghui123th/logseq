--
## VBA代码批量修改表格
##
#+BEGIN_SRC
Sub ChangeTable()
Application.Browser.Target = wdBrowseTable
    For i = 1 To ActiveDocument.Tables.Count
        ActiveDocument.Tables.Item(i).Select
        With Selection
            '表格外边框
            .Borders.OutsideLineStyle = wdLineStyleSingle
            '表格内边框
            .Borders.InsideLineStyle = wdLineStyleSingle
            '表格内边框
            .Borders(wdBorderRight).Color = wdColorAutomatic
            .Borders(wdBorderLeft).Color = wdColorAutomatic
            .Borders(wdBorderTop).Color = wdColorAutomatic
            .Borders(wdBorderBottom).Color = wdColorAutomatic
            '表格居中
            .Rows.Alignment = wdAlignRowLeft
            '表格内容居中
            .Range.Paragraphs.Alignment = wdAlignParagraphLeft
            .Range.Cells.VerticalAlignment = wdCellAlignVerticalCenter
            .Font.Name = "宋体"
            .Font.Size = 10
        End With
    Next i
End Sub
#+END_SRC
## VBA代码批量处理嵌入图片
:PROPERTIES:
:id: 602e8ea5-33b6-46bd-877f-6aafbe34e605
:END:
##
#+BEGIN_SRC 
Sub FormatPics()
Dim TuPian As InlineShape
For Each TuPian In ActiveDocument.InlineShapes
If TuPian.Type = wdInlineShapePicture Then
TuPian.LockAspectRatio = msoTrue '锁定图片的宽高比
TuPian.Width = CentimetersToPoints(14) '设置图片宽度为14CM
'TuPian.Height = CentimetersToPoints(8) '设置图片高度为8CMEnd IfNextEnd Sub
TuPian.Range.Paragraphs.Alignment = wdAlignParagraphCenter '
End If
Next
End Sub
#+END_SRC
批量
## VBA代码批量处理嵌入图片
:PROPERTIES:
:id: 602e8ea5-33b6-46bd-877f-6aa


tic
            .Borders(wdBorderBottom).Color = wdColorAutomatic
            '表格居中
            .Rows.Alignment = wdAlignRowLeft
            '表格内容居中
            .Range.Paragraphs.Alignment = wdAlignParagraphLeft          
        End With   
    Next i
End Sub
#+END_SRC
.Range.Paragraphs.Alignment = wdAlignParagraphCenter '
End If
Next
End Sub
D_SRC VBA
## VBA代码批量修改表格
##