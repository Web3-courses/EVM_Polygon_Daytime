```

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;


// LETS START THE CONTRACT
contract blog{
    // STATE VARIABLES;
    uint public counter = 0;

    // STRCUT

    // USER STRUCT --> Name, postID
    struct User{
        string name;
        uint[] postID;
    }

    // POST STRUCT --> Title, Description, UserID
    struct Post{
        string  title;
        string  description;
        address user;
    }

    // MAPPINGS

    // posts created by users
    // posts[postID] = user 1
    // posts[1] = user 2
    // postsOfUser[0x1234] = [1,2,3,5,6]

    mapping(address => uint[]) public postsOfUser;

    // user[postID] = postDetails
    mapping(uint => Post) public userPosts;

    // MODIFIERS
    modifier onlyOwner(uint _postID){
        require(msg.sender == userPosts[_postID].user,'ERROR Because you are not the owner');
        _;
    }
    // msg.sender --> 0x1232
    // posts[postID] = owner who created this partciaular post --> 0x1234

    // EVENTS
    event broadcastDetails(address indexed user, string indexed title, string indexed description);

    // FUNCTIONS
    // Create/Read/Update

    // CREATE A POST
    function createPost(string memory _title,string memory _description)
    public
    {
            userPosts[counter] = Post(_title,_description,msg.sender);
            //posts[counter] = msg.sender;
            postsOfUser[msg.sender].push(counter);
            emit broadcastDetails(msg.sender, _title,_description);
            counter++;
    }

    // READ THE POST
    function readPost(uint _id)
    view
    public
    returns(Post memory){
        return userPosts[_id];
    }

    // UPDATE THE POST
    function updatePost(uint _postID,string memory _title, string memory _description)
    public
    onlyOwner(_postID){
        // modifier
        userPosts[_postID] = Post(_title,_description,msg.sender);
    }



}


```
