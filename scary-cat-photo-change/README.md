# Download cat picture

`wget https://img.freepik.com/premium-photo/scary-cat-ai-generated_259696-3040.jpg`

# rename

`mv scary-cat-ai-generated_259696-3040.jpg scary-cat.jpg`

#Upload to bucket

`aws s3 cp scary-cat.jpg s3://tech242-henrique-first-bucket`

# Set permissions to public 

`aws s3api put-object-acl --bucket tech242-henrique-first-bucket --key scary-cat.jpg --acl public-read`

# change image
```
if grep -q 'src="/home/ubuntu/scary-cat.jpg"' /repo/springapi/src/main/resources/templates/home.html; then
	echo "Cat Image already there.
else
	echo "Changing image to scary cat picture..."
	sudo sed -i 's|<img src="/images/friday13th.jpg" alt="friday13thposter">|<img src="/home/ubuntu/scary-cat.jpg" alt="scarycatposter">|g' /repo/springapi/src/main/resources/templates/home.html
fi
```

#cd into correct repository
```
cd /repo
cd springapi
```
#
`mvn package`