const fs = require('fs');
const axios = require('axios');

const cameras = [
  {
    name: 'Lysaker',
    path: 'https://www.vegvesen.no/public/webkamera/kamera?id=424667',
  },
  {
    name: 'Sandvika',
    path: 'https://www.vegvesen.no/public/webkamera/kamera?id=424667'
  },
  {
    name: 'Gaustad',
    path: 'https://www.vegvesen.no/public/webkamera/kamera?id=410395'
  }
];



async function grab(camera) {
  console.log(`[${new Date().toLocaleString()}] Grabbing camera ${camera.name}`);
  axios({
    url: camera.path,
    headers: {
      'User-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36',
      'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8'
    },
    method: 'GET',
    responseType: 'arraybuffer', // important
  }).then((response) => {
    fs.writeFileSync(`./output/${camera.name}/${Date.now()}.jpg`, new Buffer(response.data, 'binary'));
  });
}

// Create directories at launch
cameras.forEach((el) => {
  const cameraLocalPath = `./output/${el.name}`;
  if (!fs.existsSync(cameraLocalPath)) fs.mkdirSync(cameraLocalPath);
})

// Create executor
setInterval(() => {
  cameras.forEach((camera) => {
    grab(camera);
  });
}, 15 * 60 * 1000);

// initial call
cameras.forEach((camera) => {
  grab(camera);
});