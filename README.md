import axios from 'axios';

function handleFileUpload(event) {
  const file = event.target.files[0];
  const formData = new FormData();
  formData.append('file', file);

  axios.post('https://api.tos.com/upload', formData, {
    headers: {
      'Content-Type': 'multipart/form-data'
    }
  }).then(response => {
    console.log(response);
  }).catch(error => {
    console.log(error);
  });
}
