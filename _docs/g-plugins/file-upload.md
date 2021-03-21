---
title: File Uploading
category: Plugins
order: 1
---

*Puko* provides libs to facilitate the file upload process.
You can directly upload files using the html form as shown below:

```html
<form action="" method="POST" enctype="multipart/form-data">
    <input type="file" name="filedata" />
</form>
```

---

Backend processing of file can done in controller with the File lib included in puko framework.
Let's see it in action from code below:

```
$file = Request::Files('filedata', null, true);
```

First parameter of the object instantiation is to tell the file library that `filedata` is the expected name of the data send by HTTP Request.
Second parameter is to make the alternative value if the expected data send by HTTP Request not exists. so we set `null` for it now.
Last param is boolean value if `true` to tell the File to transform data as PHP objects or `false` to keep it defaults as array.
For simplicity we will using `true` so the data retreived from $_FILE converted into objects.

If you want to add some validations, you can write the code like example below:

```php
if ($file === null) {
    throw new Exception($this->say('FILE_REQUIRED'));
}

//it will check file size and throw error if size greater than 15MB
if ($file->isSizeSmallerThan(15 * Files::MB)) {
    throw new Exception($this->say('FILE_TO_LARGE'));
}
//global is error from native PHP
if ($file->isError()) {
    throw new Exception('FILE_ERROR');
}
```

List of all method available for use in File lib:

```php
getName(); //get file name
getType(); //get file type
getTmpName(); //get temporary name of the server in the request-response cycles
isError(); //global is error from native PHP
getSize(); //get size of the file in kB
isSizeSmallerThan(float $expectations = 10 * Files::MB); //file size validation and default value set to is lower than 10MB
getFile(); //get binary file
```

For example, you can save it to database like this:

```php
$actual_data =  $file->getFile();

$model = new \plugins\model\data();

//in MySQL, column data type of "filedata" assigned to longblob
$model->filedata = $file->getFile();
$model->save();
```

You can also save the uploaded file in server directory. For example:

```php
$actual_data =  $file->getFile();

$extensions = explode('.', $actual_data);
$server_dir_path = Framework::$factory->getRoot() . '/uploads/listing';
if (!is_dir($server_dir_path)) {
    mkdir($server_dir_path);
}
$upload_path = Framework::$factory->getRoot() . '/uploads/listing/' . $file->getName();
move_uploaded_file($actual_data, $upload_path);
```
