- make sure to have functionality that a user can create an article. 

- An image is a file,can we send files with an http request?
- There is something called base64 that translates a file into a huge string

- Show how a base64 string looks like

- add an input field for the image 

```html
<input data-cy='image' placeholder='Image' type='file' name='image'>
```
- Put a debugger and make sure to get hold of the image input
```javascript
event.target.children.image.files[0]
```

- add a conditional to the method where we send of the request

```javascript
let encodedImage
if (event.target.children.image.files[0]) {
  encodedImage = await toBase64(event.target.children.image.files[0])
}
```
- now lets define the tobase64() method

```javascript
const toBase64 = (file) => new Promise((resolve, reject) => {
    const reader = new FileReader()
    reader.readAsDataURL(file)
    reader.onload = () => resolve(reader.result)
    reader.onerror = () => reject(error)
  })

```
- pass image as an argument to the create article function
- If you want to make your own preview
```javascript

//put the image into state with an onchange
<img src={URL.createObjectURL(image)}>
```