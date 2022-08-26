```


import './App.css';
import 'bootstrap/dist/css/bootstrap.min.css';
import { ethers } from "ethers";
import React from 'react';
import { useState } from 'react';

import abi from './utils/contracts/Blog.json';
import contractAddressForBlog from './utils/constants/constants.js';

const App = () => {

  // state
  const [provider,setProvider] = useState('');
  const [signer,setSigner]     = useState('');
  const [contract,setContract] = useState('');
  const [accountAddress,setAccountAddress] = useState('');

  const contractABI = abi.abi;
  const contractAddress = contractAddressForBlog;
  // account address
  // contract address
  // balance
  // provider --> alchemy/metamask ok
  // signer --> metamask because it has access to your private key ok
  // contract --> contract address and abi ok
  const [postIDs,setPostIDs]= useState(['']);
  const [post,setPost] = useState([{_title:'',_description:''}]);
  const [counter,setCounter] = useState(0);

  const connectWallet = async () =>{
    if(window.ethereum){

      // provider
      const web3Provider = new ethers.providers.Web3Provider(window.ethereum);     
      setProvider(web3Provider);
      // signer
      const web3Signer = web3Provider.getSigner(0);
      setSigner(web3Signer);
      // contract
      const blogContract = new ethers.Contract(contractAddress, contractABI, web3Signer);
      setContract(blogContract);

      await web3Provider.send("eth_requestAccounts", []).then((res)=>{
        
        setAccountAddress(res[0]);
        
      });

    }
    else{
      alert('No ethereum in window object');
    }
  }


  // form submit method

  const formSubmit = async (event) =>{

    event.preventDefault();

    const _title = event.target.title.value;
    const _description = event.target.description.value;

    // CREATING
    const posting = await contract.createPost(_title,_description); 


    // Get the counter
    const getCounter = await contract.counter();
    
    console.log(getCounter);
    //console.log(parseInt(getCounter._hex, 16));
    setCounter(getCounter._hex);

    const lastPostID = await contract.readPost(counter);
    console.log(lastPostID);

    setPost(arr => [...arr,{title:lastPostID.title,description:lastPostID.description}]);



  }

    // form2 submit method

    const formSubmit2 = async (event) =>{

      event.preventDefault();
  
      const _title = event.target.title.value;
      const _description = event.target.description.value;
      const _postID =  event.target.counter.value;

      console.log(typeof(counter));
  
      // CREATING
      const posting = await contract.updatePost(_postID,_title,_description); 
  
    }

    const readData = async (event) =>{

      event.preventDefault();
      const _postID = event.target.counter.value;

      const reading = await contract.readPost(_postID);

      console.log(reading);

      
    }


  return(
    <div className="container">
      
      <p>{accountAddress}</p>
      <p>{parseInt(counter,16)}</p>

      <button onClick={connectWallet}>Connect Wallet</button>

      <form onSubmit={formSubmit}>

        <input type="text" name="title" placeholder="Enter the title" required/><br/>
        <input type="text" name="description" placeholder="Enter the Description" required/><br/>
        <button type="submit">Submit</button>

      </form>

      <br/>
      <br/>

      <form onSubmit={formSubmit2}>

        <input type="text" name="title" placeholder="Enter the title" required/><br/>
        <input type="text" name="description" placeholder="Enter the Description" required/><br/>
        <input type="number" name="counter" required/>
        <button type="submit">Submit</button>

      </form>

      <br/>

      <form onSubmit={readData}>

        <input type="number" name="counter" required/>
        <button type="submit">Submit</button>

      </form>


      <br/>
      <table className="table">
        <thead>
          <tr>
            <th>Index</th>
            <th>Title</th>
            <th>Description</th>
          </tr>
        </thead>
        <tbody>
          {post.map((post, index) => {
            return (
              <tr key={index}>
                <td>{index}</td>
                <td>{post.title}</td>
                <td>{post.description}</td>
              </tr>
            )
          }
          )}
        </tbody>

      </table>
    </div>
  );
  
}

export default App;


```
