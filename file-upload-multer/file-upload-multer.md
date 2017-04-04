# File upload with React/redux, multer
`multer` is a middleware of node.js, which enables upload multi-forms to the host. I will use React/Redux, and multer to implement upload API for both front-end and back-end.

## Process
1. install multer, set up a back-end API for uploading
2. create front-end `form`
3. asynchronous upload `action` implementation


## Back-end API setup
<!-- multer middleware  explanation !!!!!!!!!!!!!!!!!!-->

```javascript
/* SERVER SIDE: node.js */
// setup multer: npm install --save multer

const multer = require('multer');
const upload = multer({ dest: 'uploadedDirectory/' });// uploaded files will be saved in this `dest` directory

app.post('/upload', upload.single('image'), (req, res, next) => {
  //'image' should match with 'image' data-filed-name on the front-end
  console.log(req.file);
  res.sendStatus(204);
})
```


## Create Front-end `Form`
We will create an upload form using `<input type="file" />`, then implement submit handler(`handleSubmit`) to generate a formdata to upload. Afterwards, we need to hook this data with asynchronous action using `axios`. FYI, connect is used to associate with redux actions.

```jsx
import React from 'react'
import { connect } from 'react-redux'

class UploadExercise extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleSubmit(evt) {
    evt.preventDefault();

    const data = new FormData();
    data.append('image', document.getElementById('file').files[0]);// 'image' => field-name, file => DOM name
    this.props.uploadFileToServer(data);// => associates with an asynchronous request
  }

  render () {
    return (
      <section>
        <form role="form">
          <div className="form-group">
            <input id="file" type="file" />
          </div>
          <button id="upload" type="button" onClick={this.handleSubmit}>Upload</button>
        </form>
      </section>
    )
  }
}

export default connect(null, { uploadFileToServer })(UploadExercise)
```


## Create an asynchronous action to upload files to the server-side API
<!-- TOO SIMPLE !!!!-->

```jsx
// uploadFileToServer: redux action
// npm install --save axios

const uploadFileToServer = data => dispatch =>
  axios.post('/upload', data)
    .catch(err => console.error(err))

```


