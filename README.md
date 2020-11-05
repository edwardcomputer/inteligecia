# inteligecia
clase
let knn
let extractor
let video
let estado


function setup() {
createCanvas(320,240);
video = createCapture(VIDEO).hide()
btnFeliz = createButton('Feliz')
btnTriste = createButton('Triste') 
textSize(60)  
  
  
//ml5 stuff
knn = ml5.KNNClassifier()
extractor = ml5.featureExtractor("MobileNet", ()=> {
  console.log("Extractor de MobilenetReady")
  
  btnFeliz.mousePressed(()=>{
    let feliz = extractor.infer(video)
    knn.addExample(feliz, "feliz")
    console.log("Feliz")
  })
  
  btnTriste.mousePressed(()=>{
    let triste = extractor.infer(video)
    knn.addExample(triste, "triste")
    console.log("triste")
  })
   
  
})


}
 

function draw(){
  
  
  image(video,0,0,width, height)
  if(knn.getNumLabels() >1){
     
     clasificar()
    
  }
  
  if (estado == 'feliz'){
    
   text("😀",100,100)
    
  } else if( estado == 'triste'){
   
    text("😔",100,100)
    
  }
  

}


function clasificar(){
  
  let imagen = extractor.infer(video) 
  knn.classify(imagen, (err, result)=>{
    if(result.label === 'feliz'){
      estado = 'feliz'    
    } else {
    
    estado = 'triste'
      
    }
      
  
  }) 
 
}

