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

<input type="file" onChange={handleFileUpload} />
import ftplib

ftp = ftplib.FTP('ftp.example.com', 'username', 'password')
with open('file.txt', 'rb') as f:
    ftp.storbinary('STOR file.txt', f)
ftp.quit()
import axios from 'axios';

const fileInput = document.querySelector('input[type="file"]');
const file = fileInput.files[0];
const formData = new FormData();
formData.append('file', file);

axios.post('/api/upload/', formData)
  .then(response => {
    console.log('File uploaded successfully!');
  })
  .catch(error => {
    console.error('Error uploading file:', error);
  });


import ftplib

def upload_file(request):
    if request.method == 'POST':
        file = request.FILES['file']
        with ftplib.FTP('ftp.example.com', 'username', 'password') as ftp:
            ftp.storbinary('STOR ' + file.name, file)
        return HttpResponse('File uploaded successfully!')
    else:
        return HttpResponseBadRequest('Invalid request method')

