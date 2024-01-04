# Revert changes script

First thing to be done should be to change cat image back to the Friday the 13th image.

## Change image back to the friday the 13th 

```
if grep -q 'src="/images/friday13th.jpg"' /repo/springapi/src/main/resources/templates/home.html; then
        echo "Friday the 13th image already there."
else
        echo "Changing image to friday the 13th image..."
        sudo sed -i 's|<img src="https://tech242-henrique-first-bucket.s3.eu-west-1.amazonaws.com/scary-cat.jpg" alt="scarycatposter">|<img src="/images/friday13th.jpg" alt="friday13thposter">|g' /repo/springapi/src/main/resources/templates/home.html
fi

echo "Done!"
echo ""
```

## Move into repository

```
echo"Moving into spring api..."
echo ""
cd /repo/springapi
echo ""
echo "Done!"
```

## Load package

```
echo "Loading package..."
sudo mvn package
echo ""
echo "Done!"
```

## Move back into user repository

`cd`

## Remove image from s3 bucket
```
echo "Removing image from bucket..."
echo ""
aws s3 rm s3://tech242-henrique-first-bucket/scary-cat.jpg
echo ""
echo "Done!"
```
## Remove bucket

`aws s3 rb s3://tech242-henrique-first-bucket`