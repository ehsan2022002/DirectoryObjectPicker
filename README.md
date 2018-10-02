# DirectoryObjectPicker
Active Directory Search for Windows (.Net2003 and above)

sample code for call: 

    Try
            
            ' Show dialog
            Dim picker As DirectoryObjectPickerDialog = New DirectoryObjectPickerDialog
            'picker.AllowedObjectTypes = allowedTypes;
            picker.DefaultObjectTypes = ObjectTypes.Users
            picker.AllowedLocations = Locations.EnterpriseDomain
            'picker.DefaultLocations = Locations.EnterpriseDomain ;
            picker.MultiSelect = False
            'chkMultiSelect.Checked;
            'picker.TargetComputer = txtTargetComputer.Text;
            Dim dialogResult As DialogResult = picker.ShowDialog(Me)
            If (dialogResult = dialogResult.OK) Then
                Dim results() As DirectoryObject
                results = picker.SelectedObjects
                If (results Is Nothing) Then
                    txtDominUser.Text = "Results null."
                    Return
                End If

                Dim sb As System.Text.StringBuilder = New System.Text.StringBuilder
                Dim i As Integer = 0
                Do While (i <= (results.Length - 1))
                    sb.Append(results(i).Upn)
                    Dim downLevelName As String
                    Try
                        ' downLevelName = NameTranslator.TranslateUpnToDownLevel(results[i].Upn);
                    Catch ex As Exception
                        ''downLevelName = String.Format("{0}: {1}", ex.GetType.Name, ex.Message)
                    End Try

                    'sb.Append(string.Format("Down-level Name: \t\t {0} ", downLevelName));
                   
                    i = (i + 1)
                Loop

                txtDominUser.Text = sb.ToString
            Else
                ' txtDominUser.Text = ("Dialog result: " + dialogResult.ToString)
            End If

        Catch e1 As Exception
            '' MessageBox.Show(e1.ToString)
        End Try
