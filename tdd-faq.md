# Images & Comments

## Lesson 16: [Challenge] - CarrierWave

#### Question:
> I can successfully upload images via AWS, but they are not showing up in my application. All I see where the images should be is a broken image icon.

#### Answer:
Check your AWS bucket name. If it has a period in it, that can cause problems with uploading. Your browser may stop the image from showing up over HTTPS; if you switch the URL to start with `HTTP`, your image should show up.

To fix this in your application, you can build a new AWS bucket that doesn't contain a period and use that (regenerating the  `application.yml` file, etc.). You followed the steps in the lesson correctly, but AWS has an issue with buckets with period in the name.

After adding a new bucket, you should be able to continue using your existing user and AWS keys. If for some reason that _doesn't_ work, try generating new credentials.
