import * as React from 'react';
import {
  Button,
  Text,
  View,
  StyleSheet,
  TextInput,
  TouchableOpacity,
  Alert,
  Image,   
} from 'react-native';

export default class App extends React.Component {
  constructor(props) {
    super(props);
    // console.log('constructor executed');

    this.state = {
      colorstate: 'black',
      data: [
        { id: 1, color: 'red', is_active: false, isEdited:false},
        { id: 2, color: 'orange', is_active: false, isEdited:false},
        { id: 3, color: 'green', is_active: false, isEdited:false},
        { id: 4, color: 'purple', is_active: false, isEdited:false},
        
      ],
      colorname:null,
      buttonTitle: true, 
      showtextInput: false,
      showButton: false,
      showUpdateButton: false,
      // editbuttonValue:"",
      
    }
  }
  // componentDidMount(){
  //   let colors=["white","black","yellow","orange"]
  //   let tempArr=JSON.parse(JSON.stringify(this.state.data))
  //   let foundIndex=colors.indexOf("black")
  //   console.log("foundIndex",foundIndex)
  //   let foundIndex1=tempArr.findIndex((el)=>el.color==="green")
  //   let filteredArray=tempArr.filter((el)=>el.id!==3)
  //   console.log("filteredArray-->",filteredArray)
  //   console.log("foundIndex1-->",foundIndex1)
  // }
  // componentDidMount(){
  //   let str="React"
  //   let findValue=3
  //   let arr=[{id:1},{id:2},{id:3},{id:4},{id:5},{id:6}]
  //   for(let i=0; i<arr.length; i++){
  //     console.log("arr[i]",arr[i])
  //     console.log("arr[i].id",arr[i].id)
  //     console.log("arr[i].id===6",arr[i].id===6)


  //   }
  // }

  handleButtonPress = (value,val) =>{
    // console.log('data',val)
    this.setState({colorstate: value})
    let tempdata = this.state.data;
    for (let i=0;i<tempdata.length;i++) {
      if (val===tempdata[i].id) {
        // console.log('if',val === tempdata[i].id)
        tempdata[i].is_active = true;
      } else {
        tempdata[i].is_active = false;
      }
    }
  }

  createInput = () => {
    this.setState({ showtextInput : true });
    this.setState({ showButton : true });
    this.setState({ showUpdateButton : false });
  };
 createButton = () => {
   let idvalue=this.state.data[this.state.data.length-1].id  
   if(this.state.colorname !== null && isNaN(this.state.colorname)){
    //  for(let i=0;i<this.state.data.length;i++){
    //  if(this.state.colorname!==this.state.data[i].color){
    //    console.log("if",this.state.colorname!==this.state.data[i].color)
    //    console.log("=>",this.state.data[i].color)
    //    console.log("=>",this.state.colorname)
       let newdata={id:idvalue+1,color:this.state.colorname,is_active:false}
    this.state.data.push(newdata)
        this.setState({colorname:""})
        this.setState({showButton : false});
         this.setState({showtextInput : false });
   }
    //  }
  // }
   else{
         this.state.showButton = false
   }
  
  };

  EditButton=(value)=>{
    console.log("value",value)
    this.setState({editbuttonValue:value})
    this.setState({colorname:value.color})
    // this.setState({title:"update"})
    this.setState({showButton : false});
    // console.log(showButton)
     this.setState({showtextInput : true });
     this.setState({showUpdateButton : true });
     
  }

  updateButton=()=>{
    let tempdata=this.state.data
    for(let i=0;i<tempdata.length;i++){
    if(this.state.editbuttonValue.id===tempdata[i].id){
      // console.log(this.state.editbuttonValue.id===tempdata[i].id)
      // console.log("color",tempdata[i].color)
    tempdata[i].color=this.state.colorname
    this.setState({colorname:null})
    }
  }
  }

  deleteButton = (value) =>{
    // console.log(value)
    let tempdata = this.state.data;
    let filteredArray=tempdata.filter((el)=>el.id!==value.id)
  //   console.log("filteredArray-->",filteredArray)
    // let index=tempdata.indexOf(value)
    // let del=tempdata.splice(index,1)
    // console.log(del)
      
    //  let index = tempdata.findIndex(value =>tempdata[i].id===value.id);
    //  console.log("findIndex",index)
    //  console.log(tempdata[i])
    //  if(tempdata[i].id===value.id){
    //   console.log("findIndex",index)
    //  }
    // }
   this.setState({data:filteredArray})
  
}
  
  render(){
    console.log("state",this.state.data)
    return (
      <View
        style={{
          flex: 1,
          justifyContent: 'center',
          alignItems: 'center',
          backgroundColor: this.state.colorstate,
        }}>
        <View >
          <Text
            style={{
              color: 'white',
              fontWeight: 'bold',
              fontSize: 30,
              marginBottom: 30,
            }}>
            BACKGROUND
          </Text>
          {this.state.data.map((el,index)=>{
      // console.log("el-->",el)
      return(
        <View style={{flexDirection:"row",justifyContent:"space-between"}}>
          <View
            style={{
               
              borderColor: el.is_active ? 'white' : 'black',
              borderWidth: 3,
            }}>  
           
            
              {this.state.edit? ( <TextInput
                value={this.state.colorname}
                style={{
                  backgroundColor: 'white',
                  height: 40,
                  width: 50,
                }}
                onChangeText={(value) => this.setState({colorname:value})}
              />
            ) : <Button
            title={el.color}
             onPress={() => this.handleButtonPress(el.color,el.id)}/>}
            
          </View>
          <View style={{}}>
          <TouchableOpacity
          onPress={() => this.EditButton(el)} >
              <Text style={{color:"white"}}>Edit</Text>
            </TouchableOpacity>
            </View>
          <TouchableOpacity
          onPress={() => this.deleteButton(el)} >
              <Text style={{color:"white"}}>DEL</Text>
            </TouchableOpacity>
          </View>
             )
    })}
          
            
          <View style={{ margin: 10, flexDirection: 'row' }}>
            {this.state.showtextInput ? (
              <TextInput
                value={this.state.colorname}
                style={{
                  backgroundColor: 'white',
                  height: 40,
                  width: 150,
                }}
                onChangeText={(value) => this.setState({colorname:value})}
              />
            ) : null}
             {this.state.showButton ? (<Button
              title="insert"
              onPress={ ()=>
                this.createButton()
              }           
            /> ) : null}
            {this.state.showUpdateButton ? (<Button
              title="update"
              onPress={ ()=>
                this.updateButton()
              }           
            /> ) : null}
          </View>
          <View
            style={{
              alignItems: 'center',
              justifyContent: 'center',
              margin: 10,
            }}>
            <TouchableOpacity
              onPress={() => this.createInput()}
              style={{ height: 60, width: 60, borderRadius: 30 }}>
              <Image
                source={{
                  uri: 'https://as2.ftcdn.net/v2/jpg/00/70/16/29/1000_F_70162903_5mFpUbO3ZfRyD4gslH8j2c5VxjGMKU9G.jpg',
                }}
                style={{
                  height: 60,
                  width: 60,
                  backgroundColor: 'blue',
                  borderRadius: 30,
                }}
              />
            </TouchableOpacity>
          </View>
        </View>
      </View>
    )
  }
}


