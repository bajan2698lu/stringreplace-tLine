# stringreplace-tLine
 func writeUnhandledLine()     filewriteline($hFileOpen,";~" &amp; $tline)     $i=$i+1 EndFunc  func writeCommentedLine()     $tLineOut=stringstripws($tLine, $STR_STRIPLEADING +  $STR_STRIPTRAILING)     if $tLineOut &lt;> "" Then $tLineOut=";~" &amp; $tLineOut     filewriteline($hFileOpen, $tLineOut)     $i=$i+1 EndFunc  func handleEnumBlock()     writeCommentedLine() ;~ Copy enum line     $tLine=$IDLArray[$i]     writeCommentedLine() ;~ Copy curly brace line     $tLine=$IDLArray[$i]     while stringstripws($tLine, $STR_STRIPLEADING +  $STR_STRIPTRAILING) &lt;> "};"         $tPos=getPosFirstNonWhiteSpace($tLine)         if ($tpos=0) or (stringmid($tLine,$tPos+1,2)="//") Then             writeCommentedLine()         Else             $tLine=stringleft($tLine,$tPos) &amp; "Global Const $" &amp; stringmid($tline,$tPos+1)             $tLine=stringreplace($tLine, ",","")             $tLine=stringreplace($tLine, "| ","+ $")             writeEnumLine()         EndIf         $tLine=$IDLArray[$i]     WEnd EndFunc
