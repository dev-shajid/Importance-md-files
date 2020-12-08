## Uplode File

```
import React, { useEffect, useState } from 'react'
import Axios from 'axios'
import Cookies from 'js-cookie';

const App = () => {
  const [title, setTitle] = useState("")
  const [image, setImage] = useState(null)
  const csrftoken = Cookies.get('csrftoken')
  const sendata = async () => {
    let formdata = new FormData()
    formdata.append('title', title)
    formdata.append('image', image)
    await Axios({
      method: "post",
      url: '/api/posts/',
      headers: { 'X-CSRFToken': csrftoken },
      data: formdata
    }).then((res) => {
      console.log(res);
    })
  }
  return (
    <div>
      <div>
        <input onChange={(e) => setTitle(e.target.value)} type="text" />
        <input type="file" onChange={(e) => setImage(e.target.files[0])} />
        <button onClick={sendata} >send</button>
      </div>
    </div>
  )
}

export default App

```
