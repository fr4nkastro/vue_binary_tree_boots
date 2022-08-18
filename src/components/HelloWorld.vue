<template>


<div class="d-flex justify-content-center">
<div class="card" style="width: 50vw;">
   <img :src="require(`../assets/${currentNode.value.img}`)" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">  {{currentNode.value.statement}}</h5>
    <p class="card-text"> {{currentNode.value.question}}</p>
    <div v-if="currentNode.value !=null && currentNode.getDepth()>1" class="justify-content-lg-around">
      <button class="btn btn-primary m-2" @click="onClickYes()"> Si </button>
      <button class="btn btn-primary m-2" @click="onClickNo()"> No </button>
    </div>
    
    <button class="btn btn-primary" @click="onClickBackButton()"> Anterior </button>
  </div>
</div>
</div>

</template>

<script>
import bootstrap from 'bootstrap'
import { BTreeNode, BTree } from '@dsinjs/binary-tree';
import {Step} from '../step'
export default {
  data() {
    return {
      currentNode: null,
      lastNodes:[],
      rootNode:null
    } 
  },
  methods: {
      setStep(statement, question, img) {
    let step = new Step();
    step.statement=statement;
    step.question=question;
    step.img= img;
  
    return step;
  },
  setNode(statement, question, img) {
    let step=this.setStep(statement,question, img);
    let node = new BTreeNode({value: step});
    return node;
  },
  
   onClickYes(){
    if(this.currentNode.lNode!=null){
      this.currentNode= this.currentNode.lNode;
      this.lastNodes.push(this.currentNode);
      console.log(this.currentNode);
    }
  },
   onClickNo(){
    if(this.currentNode.rNode!=null){
      this.currentNode= this.currentNode.rNode;
      this.lastNodes.push(this.currentNode);
      console.log(this.currentNode);
    }

  },
   onClickBackButton(){
    //Verificar si el currentNode es el rootNode
    if(this.currentNode!=this.rootNode){
      //Regresar al lastNodes
      this.lastNodes.pop();
      this.currentNode=this.lastNodes[this.lastNodes.length-1];
      // console.log(this.lastNodes);
    }
  }
  },
  created(){
    console.log('Created')
     let valueRoot= this.setStep(
      "Acidosis Metabólica: Nivel Del Anion GAP",
      "¿El nivel del Anion GAP es elevado?",
      '1_nivel_anion.png');
    
    let tree= new BTree(valueRoot);
    
    
    //Creación de nodos
  let node2= this.setNode(
    "Anion GAP Normal",
    "¿El GAP urinario es positivo?",
    "2_gap_urinario.jpg"
    );

  new BTreeNode({value:this.setStep})
  let node3= new BTreeNode({value:this.setStep(
    "Anion GAP elevado",
    "¿Se detecta Hipoxia tisular?",
    "3_hipoxia.jpg")})
    
  
  let node4= new BTreeNode({value:this.setStep(
    "Gap Urinario Negativo ",
    "Pérdidas digestivas: \n -Diarreas \n-Íleo \n -Adenoma velloso \n -Fístulas intestinales \n ATR Proximal (tipo II) \n Acetazomaida",
    "4_urinario_negativo.jpg")})
  node2.lNode= node4;
  
  let node5= new BTreeNode({value:this.setStep(
    "GAP urinario positivo",
    "ATR Distal (tipo I)\n ATR tipo IV \n Ciertas formas de insuficiencia renal",
    "5_urinario_positivo.jpg")})
  node2.rNode=node5;


  let node6= new BTreeNode({value:this.setStep(
    "Resultado de Hipoxia tisular",
    " Se presenta Acidosis L-Láctica",
    "6_acidosis_lactica.jpg")})
    node3.lNode=node6;

  let node7= new BTreeNode({value:this.setStep(
    "Verificación de Cuerpos Cetónicos",
    "¿Se presentan cuerpos Cetónicos?",
    "7_cetonicos.png")})
node3.rNode=node7;

  let node8= new BTreeNode({value:this.setStep(
    "Chequeo de Función Renal",
    "¿Hay función renal?",
    "8_frenal.jpg")})
    node7.rNode=node8;



  let node9= new BTreeNode({value:this.setStep(
    "Resultado de cuerpos cetónicos",
    "Se presenta Cetoacidocis",
    "9_cetoacidosis.jpg")})
    node7.lNode=node9;

  let node10= new BTreeNode({value:this.setStep(
    "Resultado de función renal",
    "Se presenta Insuficiencia Renal",
    "10_insuficiencia.jpg")})
    node8.rNode=node10;

  let node11= new BTreeNode({value:this.setStep(
    "Chequeo de GAP OSMOLAR",
    "¿El nivel de GAP OSMOLAR es normal?",
    "11_osmolar.png")})
    node8.lNode=node11;

  let node12= new BTreeNode({value:this.setStep(
    "GAP OSMOLAR bajo",
    "Posible intoxicación: \n -Etanol \n -Metanol \n -Etilenglicol",
    "12_omo_low.jpg")})
    node11.rNode=node12;

  let node13= new BTreeNode({value:this.setStep(
    "GAP OSMOLAR normal",
    "Posible intoxicación: \n -Salicilatos \n -Paraldehído",
    "13_osmo_norm.jpg")})
    node11.lNode=node13;
    //Crear la estructura del arbol binario
  tree.root.rNode=node2;
  tree.root.lNode=node3;


  //Inicialización de la navegación
  this.rootNode= tree.root; 
  this.currentNode= this.rootNode;
  this.lastNodes=[this.currentNode];

  console.log(this.rootNode.value.statement)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import'~bootstrap/dist/css/bootstrap.css'
</style>
