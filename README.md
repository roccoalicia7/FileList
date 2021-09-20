# FileList
Func _FindOldestFolder($Path, $old_new = 0)      If $old_new = Default Then $old_new = 0     Local $FileList = _FileListToArray($Path, "*.*", 2)     If @error = 1 Then         MsgBox(0, "", "No Folders Found.")         Exit     EndIf     If @error = 4 Then         MsgBox(0, "", "No Files Found.")         Exit     EndIf      Local $aLDateDiff[($FileList[0] + 1)]      For $i = 1 To UBound($FileList) - 1         Local $aDateFolder = FileGetTime($Path &amp; "\" &amp; $FileList[$i], 1, 0)         If @error Then             ;MsgBox(0, "FileGetTime Error", $Path &amp; "\" &amp; $FileList[$i])             Return 0         Else             Local $dLOldDate = ($aDateFolder[0] &amp; "/" &amp; $aDateFolder[1] &amp; "/" &amp; $aDateFolder[2] &amp; " " &amp; $aDateFolder[3] &amp; ":" &amp; $aDateFolder[4] &amp; ":" &amp; $aDateFolder[5])             $aLDateDiff[$i] = _DateDiff("s", $dLOldDate, _NowCalc())         EndIf     Next     If $old_new = 0 Then         Return $FileList[_ArrayMaxIndex($aLDateDiff)]     Else         Return $FileList[_ArrayMinIndex($aLDateDiff)]     EndIf  EndFunc   ;==>_FindOldestFolder
