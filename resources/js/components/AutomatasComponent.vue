<template>
    <div>
        <h1 class="text-center textocolor fredoka mt-5 pt-4">Crear Autómata</h1>
        <div class="row justify-content-center" >
            <div class="grafo1 col-md-3 mx-4 card cardaux" v-if="!representacion1">
                <div class="container-fluid mr-4">
                    <div class="row justify-content-center ml-1" v-if="!automataCreate">
                        
                            <div class="col-md-6 my-4"><button class="btn btn-success info textocolor" @click="selectAFD">Crear AFD</button></div>
                            <div class="col-md-6 my-4"><button class="btn btn-success info textocolor" @click="selectAP">Crear AP's</button></div>
                        
                    </div>

                </div>
                <!--AFD-->
                <div class="container-fluid py-4 mr-4" v-if="option===1">
                    <h3 class="mt-2">Autómata Finito Determinista (AFD)</h3>
                    <hr>
                    <div class="row text-center my-4" v-if="!selected">
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="createEstado">Añadir Estado</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="createTransicion">Añadir Transición</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="representacion">Modificar Estado Final</button>
                        </div>
                    </div>
                    <div class="row text-center" v-if="!selected">
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="showAnalisisPalabra">Analizar Palabra</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-danger">Eliminar Autómata</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-warning" @click="backInicio"> Volver al Inicio</button>
                        </div>                       
                    </div>

                    <button class="btn btn-success btn-sm" v-if="selected" @click="back">Volver</button>
                    <div class="my-4" v-if="creaEstado">
                        <div>
                            <form @submit.prevent="crearEstado">
                                <div class="form-group">
                                    <label for="id">Ingrese el id: </label>
                                    <input type="number" min="0" class="form-control" v-model="estadoAutomataAFD.id">
                                </div>
                                <div class="text-center">
                                    <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                </div>
                            </form>
                        </div>
                    </div>

                    <div class="my-3" v-if="createTrans">
                        <form @submit.prevent="crearTransicion">
                            <div class="form-group">
                                <label>Ingrese el id del estado inicial de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAutomataAFD.from">
                            </div>
                            <div class="form-group">
                                <label>Ingrese el id del estado final de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAutomataAFD.to">
                            </div>
                            <div class="form-group">
                                <label>Ingrese carácter de la transición: </label>
                                <input type="text" minlength="1" class="form-control" v-model="transicionAutomataAFD.label">
                            </div>

                            <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                        </form>
                    </div> 


                    <div class="col-md-12 my-4" v-if="analizarPalabra">
                        <form @submit.prevent="analizarCadenaAFD">
                            <div class="form-group">
                                <label>Ingrese la palabra: </label>
                                <input type="text" class="form-control" v-model="cadena">
                            </div>
                            <button class="btn btn-success btn-sm" type="submit">Consultar Palabra</button>
                        </form>
                    </div> 
                </div>
                <!--AFD-->



                <!--AP-->
                <div class="container-fluid py-4 mr-4" v-if="option===2">
                    <h3 class="mt-2">Autómatas de Pila (AP)</h3>
                    <div class="row text-center my-4" v-if="showAps">
                        <div class="col-md-6">
                            <button class="btn btn-sm btn-success" @click="createAP1">Crear AP 1</button>
                        </div>
                        <div class="col-md-6">
                            <button class="btn btn-sm btn-success"  @click="createAP2">Crear AP 2</button>
                        </div>
                    </div>
                    <div class="row my-2" v-if="showAps">
                        <div class="col-md-4"></div>
                        <div class="col-md-4 text-center">
                            <button class="btn btn-sm btn-warning" @click="backInicio">Volver al Inicio</button>
                        </div>
                    </div>

                    <div class="row text-center my-4" v-if="!selected">
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="createEstado">Añadir Estado</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="createTransicion">Añadir Transición</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="representacion">Modificar Estado Final</button>
                        </div>
                    </div>

                    <button class="btn btn-success btn-sm mt-3" v-if="selected2" @click="back">Volver</button>

                    <div class="row text-center" v-if="!selected">
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-success" @click="showAnalisisPalabra">Analizar Palabra</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-danger">Eliminar Autómata</button>
                        </div>
                        <div class="col-md-4">
                            <button class="btn btn-sm btn-warning" @click="backToAp"> Volver</button>
                        </div>                       
                    </div>




                    <div class="my-4" v-if="creaEstado">
                        <div>
                            <form @submit.prevent="crearEstado" v-if="apSeleccionado===1">
                                <div class="form-group">
                                    <label for="id">Ingrese el id: </label>
                                    <input type="number" min="0" class="form-control" v-model="estadoAP1.id">
                                </div>
                                <div class="text-center">
                                    <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                </div>
                            </form>

                            <form @submit.prevent="crearEstado" v-if="apSeleccionado===2">
                                <div class="form-group">
                                    <label for="id">Ingrese el id: </label>
                                    <input type="number" min="0" class="form-control" v-model="estadoAP2.id">
                                </div>
                                <div class="text-center">
                                    <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                                </div>
                            </form>
                        </div>
                    </div>

                    <div class="my-3" v-if="createTrans">
                        <form @submit.prevent="crearTransicion" v-if="apSeleccionado===1">
                            <div class="form-group">
                                <label>Ingrese el id del estado inicial de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAP1.from">
                            </div>
                            <div class="form-group">
                                <label>Ingrese el id del estado final de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAP1.to">
                            </div>
                            <div class="form-group">
                                <label>Ingrese carácter de la transición: </label>
                                <input type="text" minlength="1" class="form-control" v-model="transicionAP1.label">
                            </div>
                            <div class="form-group">
                                <label>Push(): </label>
                                <input type="text" minlength="1" class="form-control" placeholder="dejar vacío para epsilon" v-model="pilaAP.agrega">
                            </div>
                            <div class="form-group">
                                <label>Pop(): </label>
                                <input type="text" minlength="1" class="form-control" placeholder="dejar vacío para epsilon" v-model="pilaAP.elimina">
                            </div>

                            <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                        </form>

                        <form @submit.prevent="crearTransicion" v-if="apSeleccionado===2">
                            <div class="form-group">
                                <label>Ingrese el id del estado inicial de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAP2.from">
                            </div>
                            <div class="form-group">
                                <label>Ingrese el id del estado final de la transición:</label>
                                <input type="number" min="0" class="form-control" v-model="transicionAP2.to">
                            </div>
                            <div class="form-group">
                                <label>Ingrese carácter de la transición: </label>
                                <input type="text" minlength="1" class="form-control" v-model="transicionAP2.label">
                            </div>
                            <div class="form-group">
                                <label>Push(): </label>
                                <input type="text" minlength="1" class="form-control" placeholder="dejar vacío para epsilon" v-model="pilaAP.agrega">
                            </div>
                            <div class="form-group">
                                <label>Pop(): </label>
                                <input type="text" minlength="1" class="form-control" placeholder="dejar vacío para epsilon" v-model="pilaAP.elimina">
                            </div>

                            <button class="btn btn-success btn-sm" type="submit">Agregar</button>
                        </form>
                    </div> 

                    <div class="col-md-12 my-4" v-if="analizarPalabra">
                        <form @submit.prevent="" v-if="apSeleccionado===1">
                            <div class="form-group">
                                <label>Ingrese la palabra: </label>
                                <input type="text" class="form-control">
                            </div>
                            <button class="btn btn-success btn-sm" type="submit">Consultar Palabra</button>
                        </form>

                        <form @submit.prevent="" v-if="apSeleccionado===2">
                            <div class="form-group">
                                <label>Ingrese la palabra: </label>
                                <input type="text" class="form-control">
                            </div>
                            <button class="btn btn-success btn-sm" type="submit">Consultar Palabra</button>
                        </form>
                    </div>

                </div>
                <!--AP-->
            </div>

            <!--MODIFICAR ESTADOS FINALES-->
            <div class="grafo1 col-md-5 mx-3 card cardaux my-3" v-if="representacion1">
                <hr>
                <div>

                    <h3 class="text-center fredoka my-3" v-if="option===1">Tabla de estados autómata Finito Determinista</h3>
                    <table class="table table-striped table-dark" aria-describedby="estados1" v-if="option===1">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">Estado</th>
                                <th scope="col">Final</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(item,index) in estadosAutomataAFD" :key="index" v-show="index!=0">
                                <td>{{index}}</td>
                                <td>{{item.label}}</td>
                                <td>
                                    <div>
                                        <input type="checkbox" name="state" id="state" @click="marcarFinal(item.id)" :checked="estadosAutomataAFD[index].final">
                                        <label for="state">Estado Final</label>
                                    </div>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                    <h3 class="text-center fredoka my-3" v-if="option===2">Tabla de estados autómata de Pila 1</h3>
                    <table class="table table-striped table-dark" aria-describedby="estados1" v-if="option===2">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">Estado</th>
                                <th scope="col">Final</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>a</td>
                                <td>a</td>
                                <td>a</td>
                            </tr>
                        </tbody>
                    </table>
                    <h3 class="text-center fredoka my-3" v-if="option===2">Tabla de estados autómata de Pila 2</h3>
                    <table class="table table-striped table-dark" aria-describedby="estados1" v-if="option===2">
                        <thead>
                            <tr>
                                <th scope="col">#</th>
                                <th scope="col">Estado</th>
                                <th scope="col">Final</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>a</td>
                                <td>a</td>
                                <td>a</td>
                            </tr>
                        </tbody>
                    </table>
                    <button class="btn btn-success btn-sm mb-3 text-right" type="submit" @click="representacionBack">Guardar</button>
                    

                </div>
            </div>
            <!--MODIFICAR ESTADOS FINALES-->

            <!--REPRESENTACION AUTOMATAS-->
            <div class="grafo1 col-md-8 card cardaux">
                <h3 class="text-center fredoka my-2">Representación</h3>
                <div class="row">
                    <div class="col-md-12" v-if="option===1">
                        <h4 class="text-center fredoka my-3" >Autómata Finito Determinista</h4>
                        <div id="AFD" class="mb-3" style="border:1px solid lightgray;"></div>
                    </div>

                    <div class="col-md-6" v-if="option===2">
                        <h4 class="text-center fredoka my-3">Autómata de Pila 1</h4>
                        <div  id="AP1" class="mb-3" style="border:1px solid lightgray;"></div>
                    </div>
                    <div class="col-md-6" v-if="option===2">
                        <h4 class="text-center fredoka my-3">Autómata de Pila 2</h4>
                        <div id="AP2" class="mb-3" style="border:1px solid lightgray;"></div>
                    </div>
                </div>
            </div>

            <!--REPRESENTACION AUTOMATAS-->
        </div>

        <h1 class="text-center fredoka textocolor my-4">Operaciones</h1>
        <div class="row justify-content-center">
            <div class="card cardaux4 col-md-10 rounded-top">
                <div class="btn-group justify-content-center" role="group">
                    <a href="#"><button class="btn btn-secondary" @click="mostrarOP1">Expresión Regular</button></a>
                    <a href="#"><button class="btn btn-secondary" @click="mostrarOP2">Concatenación de AP's</button></a>
                    <a href="#"><button class="btn btn-secondary" @click="mostrarOP3">Unión de AP's</button></a>
                </div>
            </div>

            <!--CASO 1: EXPRESIÓN REGULAR-->
            <div class="cardaux2 col-md-10" v-if="opcion===1">
                <h3 class="text-center fredoka textocolor my-3">Expresión Regular</h3>
            </div>
            <div class="card cardaux3 col-md-10 rounded-bottom mb-3" v-if="opcion===1">
                <div class="container my-3">
                    <button class="btn btn-success" @click="encontrarExpresionRegular">Mostrar expresion regular</button>
                    aaaaaaaaaaaaaa
                </div>
            </div>

            <!--CASO 2: CONCATENACIÓN-->
            <div class="cardaux2 col-md-10" v-if="opcion===2">
                <h3 class="text-center fredoka textocolor my-3">Concatenación de AP'S</h3>
            </div>
            <div class="card cardaux3 col-md-10 rounded-bottom mb-3" v-if="opcion===2">
                <div class="container my-3">

                    aaaaaaaaaaaaaa
                </div>
            </div>

            <!--CASO 3: UNION-->
            <div class="cardaux2 col-md-10" v-if="opcion===3">
                <h3 class="text-center fredoka textocolor my-3">Unión de AP's</h3>
            </div>
            <div class="card cardaux3 col-md-10 rounded-bottom mb-3" v-if="opcion===3">
                <div class="container my-3">
                    <button class="btn btn-success" @click="unionAp">Mostrar Unión UWU</button>
                    <div id="APUNIDOS" style="border:1px solid lightgray;"></div>
                    aaaaaaaaaaaaaa
                </div>
            </div>




        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            estadosAutomataAFD:[{id: 'inicio', label: 'inicio', color:'#75616b47', final: false}],
            estadoAutomataAFD:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAutomataAFD:[],
            transicionAutomataAFD:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},

            estadosAP1:[{id: 'inicio', label: 'inicio', color:'#75616b47', final: false}],
            estadoAP1:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAP1:[],
            transicionAP1:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},
            
            pilaAP:{agrega:'',elimina:''},
            pila1:[],
            pila2:[],

            estadosAP2:[{id: 'inicio', label: 'inicio', color:'#75616b47', final: false}],
            estadoAP2:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAP2:[],
            transicionAP2:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},
            


            expresionRegularAFD:'',
            
            estadosAutomataUnionAP:[],
            estadoAutomataUnionAP:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAutomataUnionAP:[],
            transicionAutomataUnionAP:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},

            estadosAutomataConcatenacionAP:[],
            estadoAutomataConcatenacionAp:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAutomataConcatenacionAP:[],
            transicionAutomataConcatenacionAp:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},


            alfabetoAFD:[],
            alfabetoAP1:[],
            alfabetoAP2:[],

            cadena:'',

            selected:false,
            selected2:false,
            automataCreate:false,
            option:'',
            opcion:0,
            representacion1:false,
            analizarPalabra:false,
            volverInicio:false,
            createTrans:false,
            creaEstado:false,
            showAps:false,
            apSeleccionado:0,
        }
    },

    created(){

    },

    methods:{

        selectAFD(){
            this.automataCreate=true;
            this.option=1;
        },

        selectAP(){
            this.automataCreate=true;
            this.selected=true;
            this.showAps=true;
            this.option=2;
        },

        createEstado(){
            this.creaEstado=true;
            this.selected=true;    
            this.selected2=true;  
            this.createTrans=false;
        },

        createTransicion(){
            this.createTrans=true;
            this.selected=true;
            this.selected2=true;
            this.creaEstado=false;
        },

        representacion(){
            this.representacion1=true;
        },

        representacionBack(){
            this.representacion1=false;
            this.drawAutomata();
        },

        showAnalisisPalabra(){
            this.analizarPalabra=true;
            this.createTrans=false;
            this.selected=true;
            this.selected2=true;
        },

        back(){
            this.selected=false;
            this.createTrans=false;
            this.creaEstado=false;
            this.analizarPalabra=false;
            this.selected2=false;
        },

        backInicio(){
            this.automataCreate=false;
            this.creaEstado=false;
            this.option=0;
            this.selected=false;
        },

        backToAp(){
            this.selected=true;
            this.showAps=true;
        },

        createAP1(){
            this.selected=false;
            this.showAps=false;
            this.apSeleccionado=1;
        },

        createAP2(){
            this.selected=false;
            this.showAps=false;
            this.apSeleccionado=2;
        },

        mostrarOP1(){
            this.opcion=1;
        },

        mostrarOP2(){
            this.opcion=2;
        },

         mostrarOP3(){
            this.opcion=3;
        },

        existeEstadoTransicion(estados, transicion)
        {
            var existeFrom=false;
            var existeTo= false;
            for(var i=0; i<estados.length;i++)
            {
                if(estados[i].id===transicion.from)
                {
                    existeFrom=true;
                }
                else{
                    if(estados[i].id!=transicion.from && existeFrom===true)
                    {
                        existeFrom=true;
                    }
                    else{
                        if(estados[i].id!=transicion.from && existeFrom===false)
                        {
                            existeFrom=false;
                        }
                    }
                }
            }
            for(var j=0; j<estados.length;j++)
            {
                if(estados[j].id===transicion.to)
                {
                    existeTo=true;
                }
                else{
                    if(estados[j].id!=transicion.to && existeTo===true)
                    {
                        existeTo=true;
                    }
                    else{
                        if(estados[j].id!=transicion.to && existeTo===false)
                        {
                            existeTo=false;
                        }
                    }
                }
            }

            if(existeFrom && existeTo)
            {
                return true;
            }
            else{
                return false;
            }
        },
    
        crearTransicion(){
            if(this.option===1)
            {
                if(this.transicionAutomataAFD.from ==='' || this.transicionAutomataAFD.to ==='')
                {
                    swal("Estados no ingresados. Rellene todos los campos antes de continuar",{
                        className: "alertas",
                        button: "Aceptar",
                        title: "Aviso",
                        icon: "warning"
                    });
                    return;
                }
                for( var i =0; i<this.transicionesAutomataAFD.length; i++)
                {
                    if(this.transicionesAutomataAFD[i].from===this.transicionAutomataAFD.from && this.transicionesAutomataAFD[i].label === this.transicionAutomataAFD.label)
                    {
                        swal("La transición ya existe. Ingrese otra",{
                            className: "alertas",
                            button: "Aceptar",
                            title: "Aviso",
                            icon: "warning"
                        });
                        return;

                    }
                } 
                if(!this.existeEstadoTransicion(this.estadosAutomataAFD, this.transicionAutomataAFD))
                {
                    swal("Los estados ingresados no existen. Ingrese otros estados para generar la transición",{
                        className: "alertas",
                        button: "Aceptar",
                        title: "Aviso",
                        icon: "warning",
                    });
                    return;
                } 
                if(this.existeTransicionAFD(this.transicionesAutomataAFD,this.transicionAutomataAFD))
                {
                    swal("La transición ya existe. Ingrese otra",{
                        className: "alertas",
                        button: "Aceptar",
                        title: "Aviso",
                        icon: "warning",
                    });
                    return;
                }

                for(var t=0; t<this.transicionesAutomataAFD.length;t++)
                {
                    if(this.transicionesAutomataAFD[t].from===this.transicionAutomataAFD.from && this.transicionesAutomataAFD[t].label!= this.transicionAutomataAFD.label && this.transicionesAutomataAFD[t].to ===this.transicionAutomataAFD.to){
                        var aux=[this.transicionesAutomataAFD[t].label, this.transicionAutomataAFD.label];
                        console.log("aux: ",aux);
                        this.transicionesAutomataAFD[t].label= aux[0]+ '+'+ aux[1];
                        
                        this.drawAutomata();
                        return;
                    }
                }

                this.addCaracterToAlfabeto();
                
                this.transicionesAutomataAFD.push(this.transicionAutomataAFD);
                this.transicionAutomataAFD={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}}; 
            }
            else{
                if(this.apSeleccionado===1)
                {
                    if(this.transicionAP1.from ==='' || this.transicionAP1.to ==='')
                    {
                        swal("Estados no ingresados. Rellene todos los campos antes de continuar",{
                            className: "alertas",
                            button: "Aceptar",
                            title: "Aviso",
                            icon: "warning"
                        });
                        return;
                    }
                    for( var i =0; i<this.transicionesAP1.length; i++)
                    {
                        if(this.transicionesAP1[i].from===this.transicionAP1.from && this.transicionesAP1[i].label === this.transicionAP1.label)
                        {
                            swal("La transición ya existe. Ingrese otra",{
                                className: "alertas",
                                button: "Aceptar",
                                title: "Aviso",
                                icon: "warning"
                            });
                            return;

                        }
                    }
                    if(!this.existeEstadoTransicion(this.estadosAP1, this.transicionAP1))
                    {
                        swal("Los estados ingresados no existen. Ingrese otros estados para generar la transición",{
                            className: "alertas",
                            button: "Aceptar",
                            title: "Aviso",
                            icon: "warning",
                        });
                        return;
                    }
                    else{
                        
                        this.addCaracterToAlfabeto();
                        this.transicionesAP1.push(this.transicionAP1);
                        this.pilaAPs(this.pilaAP,this.pila1,this.transicionesAP1);
                        this.pilaAp={agrega:'',elimina:''};
                        this.transicionAP1={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};

                    }
                }
                else{
                    if(this.apSeleccionado===2)
                    {
                        if(this.transicionAP2.from ==='' || this.transicionAP2.to ==='')
                        {
                            swal("Estados no ingresadow. Rellene todos los campos antes de continuar",{
                                className: "alertas",
                                button: "Aceptar",
                                title: "Aviso",
                                icon: "warning"
                            });
                            return;
                        }
                        for( var i =0; i<this.transicionesAP2.length; i++)
                        {
                            if(this.transicionesAP2[i].from===this.transicionAP2.from && this.transicionesAP2[i].label === this.transicionAP2.label)
                            {
                                swal("La transición ya existe. Ingrese otra",{
                                    className: "alertas",
                                    button: "Aceptar",
                                    title: "Aviso",
                                    icon: "warning"
                                });

                            }
                        }
                        if(!this.existeEstadoTransicion(this.estadosAP2, this.transicionAP2))
                        {
                            swal("Los estados ingresados no existen. Ingrese otros estados para generar la transición",{
                                className: "alertas",
                                button: "Aceptar",
                                title: "Aviso",
                                icon: "warning",
                            });
                            return;
                        }
                        this.addCaracterToAlfabeto();
                        this.transicionesAP2.push(this.transicionAP2);
                        this.pilaAPs(this.pilaAP,this.pila2,this.transicionesAP2);
                        this.transicionAP2={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
                    }
                }
            }
            this.drawAutomata();
        },

        existeTransicionAFD(transiciones,transicion){
            var existe= false;
            var caracteres= [];
            var aux;

            for(var i=0; i< transiciones.length;i++){
                if(transiciones[i].from===transicion.from && transiciones[i].to===transicion.to)
                {
                    if(transiciones[i].label.includes('+'))
                    {
                        aux=transiciones[i].label;
                        caracteres=aux.split('+');
                        for(var j=0; j<caracteres.length;j++)
                        {
                            if(caracteres[j]===transicion.label)
                            {
                                return true;
                            }
                        }
                        return false;
                    }
                }
            }

        },

        pilaAPs(pilaAP,pila,transiciones){
            if(pila.length<1){
                pila.push('P')                
                if(pilaAP.agrega==='' && pilaAP.elimina===''){
                    for(let k=0;k<transiciones.length;k++){
                        if(transiciones[k].from!='inicio'){
                            let nT=transiciones[k].label +  '|' + 'E' + '|' + 'E' 
                            console.log("nT",nT);
                            transiciones[k].label= nT;
                            nT = ''
                        }
                        console.log("Epsilon");
                    }
                }
                if(pilaAP.agrega!='' && pilaAP.elimina==''){
                    for(let i=0;i<transiciones.length;i++){
                        
                        if(transiciones[i].from!='inicio'){

                            console.log("agrega: ",pilaAP.agrega);
                            console.log("transiciones ap1 label",transiciones[i].label);
                            let newT = transiciones[i].label + '|' + 'E' + '|' + pilaAP.agrega;
                            console.log("newT:",newT);
                            transiciones[i].label= newT;
                            newT = ''
                            //funcion agregareliminar
                            //this.pila1.push(this.pilaAP1.agrega)
                            pilaAP.agrega=''
                        }
                    }    
                }
                if(pilaAP.elimina!='' && pilaAP.agrega==''){
                    console.log("pop()", pilaAP.elimina);
                    for(let j=1;j<transiciones.length;j++){
                        console.log("transiciones ap1",transiciones[j]);
                        let newT = transiciones[j].label + '|' + pilaAP.elimina + '|' +'E'
                        console.log("newT:",newT);
                        transiciones[j].label= newT;
                        newT = '' 
                    }
                    //funcion agregareliminar
                    //this.pila1.pop(this.pilaAP1.elimina)
                    pilaAP.elimina=''
                }
                if(pilaAP.agrega!='' && pilaAP.elimina!=''){
                    console.log("agrega: ", pilaAP.agrega, ", elimina: ", pilaAP.elimina);
                    for(let z=0;z< transiciones.length;z++){
                        if(transiciones[z].from!='inicio' && !transiciones[z].label.includes('|')){
                            console.log("entramos perrito");
                            let newElim = transiciones[z].label + '|' + pilaAP.elimina + '|' + pilaAP.agrega
                            console.log("newElim", newElim);
                            transiciones[z].label = newElim;
                            newElim='';
                            //funcion agregareliminar
                            //this.pila1.pop(this.pilaAP1.elimina)
                            //this.pila1.push(this.pilaAP1.agrega)
                            pilaAP.agrega=''
                            pilaAP.elimina=''               
                        }
                    }
                }
                console.log("pila",pilaAP);
                console.log("pila1",pila);
            }
            else{
                if(pilaAP.agrega==='' && pilaAP.elimina===''){
                    for(let m=0;m<transiciones.length;m++){
                        if(transiciones[m].from!='inicio' && !transiciones[m].label.includes('|')){
                            let nT1=transiciones[m].label +  '|' + 'E' + '|' + '|' + 'E' + '|' 
                            console.log("nt1",nT1);
                            transiciones[m].label= nT1;
                            nT1 = ''
                        }
                        console.log("Epsilon");
                    }
                }
                if(pilaAP.agrega!='' && pilaAP.elimina==''){                   
                    for(let f=0;f<transiciones.length;f++){                        
                        if(transiciones[f].from!='inicio' && !transiciones[f].label.includes('|')){
                            console.log("agrega: ",pilaAP.agrega);
                            console.log("transiciones ap1 label",transiciones[f].label);
                            let newT1 = transiciones[f].label + '|' + 'E' + '|' + pilaAP.agrega;
                            console.log("newT1:",newT1);
                            transiciones[f].label= newT1;
                            newT1 = ''
                            //funcion agregareliminar
                            //this.pila1.push(this.pilaAP1.agrega)
                            pilaAP.agrega=''
                        }
                    }                    
                }
                if(pilaAP.elimina!='' && pilaAP.agrega==''){
                    console.log("pop()", pilaAP.elimina);
                    for(let d=1;d<transiciones.length;d++){
                        if(transiciones[d].from!='inicio' && !transiciones[d].label.includes('|')){
                            console.log("transiciones ap1",transiciones[d]);
                            let newT2 = transiciones[d].label + '|' + pilaAP.elimina + '|' +'E'
                            console.log("newT2:",newT2);
                            transiciones[d].label= newT2;
                            newT2 = ''                             
                            //funcion agregareliminar
                            //this.pila1.pop(this.pilaAP1.elimina)
                            pilaAP.elimina=''
                        }
                    }
                }
                if(pilaAP.agrega!='' && pilaAP.elimina!=''){
                    console.log("Vienen llenitos");      
                    console.log("agrega: ", pilaAP.agrega, ", elimina: ", pilaAP.elimina);
                    for(let o=0;o< transiciones.length;o++){
                        if(transiciones[o].from!='inicio' && !transiciones[o].label.includes('|')){
                            console.log("entramos perrito");
                            let newElim1 = transiciones[o].label + '|' + pilaAP.elimina + '|' + pilaAP.agrega
                            console.log("newElim1", newElim1);
                            transiciones[o].label = newElim1;
                            newElim1='';
                            //funcion agregareliminar(elimina || agrega )
                            //this.pila1.pop(this.pilaAP1.elimina)
                            //this.pila1.push(this.pilaAP1.agrega)
                            pilaAP.agrega=''
                            pilaAP.elimina=''                           
                        }
                    }
                }
                console.log("pila",pilaAP);
                console.log("pila1",pila);
            }
            
        },

        unionAp(){
            this.estadosAP1.splice(0,1);
            this.estadosAP2.splice(0,1);
            this.transicionesAP1.splice(0,1);
            this.transicionesAP2.splice(0,1);
            this.copiarAutomata(this.estadosAP1,this.transicionesAP1,this.estadosAutomataUnionAP,this.transicionesAutomataUnionAP);
            this.estadosAutomataUnionAP= this.estadosAutomataUnionAP.concat(this.estadosAP2);
            this.transicionesAutomataUnionAP= this.transicionesAutomataUnionAP.concat(this.transicionesAP2);
            
            this.estadoAutomataUnionAP.id='inicio';
            this.estadoAutomataUnionAP.label='inicio';
            this.estadoAutomataUnionAP.color='#75616b47';
            this.estadosAutomataUnionAP.push(this.estadoAutomataUnionAP);
            this.transicionAutomataUnionAP.from='inicio';
            this.transicionAutomataUnionAP.to=this.estadosAP1[0].id;
            this.transicionAutomataUnionAP.label='E|E|E';
            this.transicionesAutomataUnionAP.push(this.transicionAutomataUnionAP);
            this.transicionAutomataUnionAP={from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}}
            this.transicionAutomataUnionAP.from='inicio';
            this.transicionAutomataUnionAP.to=this.estadosAP2[0].id;
            this.transicionAutomataUnionAP.label='E|E|E';
            this.transicionesAutomataUnionAP.push(this.transicionAutomataUnionAP);
            console.log(this.transicionesAutomataUnionAP);
            console.log(this.estadosAutomataUnionAP);
            this.drawAutomata();
        },

        copiarAutomata(estadosIn,transicionesIn, estadosOut,transicionesOut)
        {
            var estado={id:'', label:'',color:'#C52C0B', final:false, shape:'ellipse'};
            var transiciones={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
            for(var i=0; i<estadosIn.length;i++)
            {
                estado.id= estadosIn[i].id;
                estado.label= estadosIn[i].label;
                estado.color= estadosIn[i].color;
                estado.final= estadosIn[i].final;
                estado.shape= estadosIn[i].shape;
                estadosOut.push(estado);
                estado={id:'', label:'',color:'#C52C0B', final:false, shape:'ellipse'};
            }
            for(var j=0; j<transicionesIn.length; j++)
            {
                transiciones.from= transicionesIn[j].from;
                transiciones.label= transicionesIn[j].label;
                transiciones.to= transicionesIn[j].to;
                transicionesOut.push(transiciones);
                transiciones={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
            }
        },

        addCaracterToAlfabeto(){
            var existe=false;
            if(this.option===1)
            {
                for(var i=0; i<this.transicionAutomataAFD.length; i++)
                {
                    if(existe===true && this.transicionAutomataAFD.label!= this.transicionesAutomataAFD[i].label)
                    {
                        existe=true;
                    }
                    else{
                        if(this.transicionesAutomataAFD[i].label===this.transicionAutomataAFD.label && existe===false)
                        {
                            existe=true;
                        }
                        else{
                            if(this.transicionesAutomataAFD[i].label!=this.transicionAutomataAFD.label && existe==false)
                            {
                                existe=false;
                            }
                        }
                    }
                }

                if(!existe)
                {
                    this.alfabetoAFD.push(this.transicionAutomataAFD.label);
                }
                console.log("Alfabeto AFD: ",this.alfabetoAFD);
            }
            else{
                if(this.apSeleccionado===1)
                {
                    for(var j=0; j<this.transicionesAP1.length;j++)
                    {
                        if(existe===true && this.transicionAP1.label!= this.transicionesAP1[j].label)
                        {
                            existe=true;
                        }
                        else{
                            if(this.transicionesAP1[j].label === this.transicionAP1.label)
                            {
                                existe=true;
                            }
                            else{
                                existe=false;
                            }
                        }
                    }

                    if(!existe)
                    {
                        this.alfabetoAP1.push(this.transicionAP1.label);
                    }

                }
                else{
                    if(this.apSeleccionado===2)
                    {
                        for(var k=0; k<this.transicionesAP2; k++)
                        {
                            if(existe===true && this.transicionAP2.label!= this.transicionesAP2[k].label)
                            {
                                existe=true;
                            }
                            else{
                                if(this.transicionesAP2[k].label=== this.transicionAP2.label)
                                {
                                    existe=true;
                                }
                                else{
                                    existe=false;
                                }
                            }
                        }
                        if(!existe)
                        {
                            this.alfabetoAP2.push(this.transicionAP2.label);
                        }
                    }
                }
            }
        },

        estadosDistintos(estados,estado)
        {
            for(var i=0; i<estados.length;i++)
            {
                if(estados[i].id===estado.id)
                {
                    return false;
                }
            }
            return true;
        },

        crearEstado(){
            var aux= {id:'inicio', label:'inicio',color:'#75616b47', final:false};

            if(this.option===1)
            {
                if(this.estadoAutomataAFD.id==='')
                {
                    swal("Por favor, ingrese un id",{
                        className: "alertas",
                        button: "Aceptar",
                        icon: "warning",
                        title: "Aviso",
                    });
                    return;
                }
                if(this.existeEstado(this.estadosAutomataAFD, this.estadoAutomataAFD))
                {
                    swal("El estado ya existe. Ingrese un estado con otro id.",{
                        className: "alertas",
                        button: "Aceptar",
                        icon: "warning",
                        title: "Aviso",
                    });
                    return;
                }
                if(this.estadosAutomataAFD.length===0)
                {
                    this.estadosAutomataAFD.push(aux);
                }
                this.estadoAutomataAFD.label=this.estadoAutomataAFD.id;
                if(this.estadosAutomataAFD.length===1)
                {
                    this.estadosAutomataAFD.push(this.estadoAutomataAFD);
                    this.transicionAutomataAFD.from='inicio';
                    this.transicionAutomataAFD.label='E';
                    this.transicionAutomataAFD.to= this.estadoAutomataAFD.id;
                    this.transicionesAutomataAFD.push(this.transicionAutomataAFD);
                    this.transicionAutomataAFD= {from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
                    this.estadoAutomataAFD= {id:'', label:'',color:'#C52C0B' ,final:false};
                    this.drawAutomata();
                    return;
                }
                else{
                    this.estadosAutomataAFD.push(this.estadoAutomataAFD);
                    this.estadoAutomataAFD= {id:'', label:'',color:'#C52C0B' ,final:false};
                    this.drawAutomata();
                }
            }
            else{
                if(this.apSeleccionado===1)
                {
                    if(this.estadoAP1.id==='')
                    {
                        swal("Por favor, ingrese un id",{
                            className: "alertas",
                            button: "Aceptar",
                            icon: "warning",
                            title: "Aviso",
                        });
                        return;
                    }
                    if(this.existeEstado(this.estadosAP1,this.estadoAP1))
                    {
                        swal("El estado ya existe. Ingrese un estado con otro id.",{
                            className: "alertas",
                            button: "Aceptar",
                            icon: "warning",
                            title: "Aviso",
                        });
                        return;
                    }
                    if(this.estadosAP1.length===0)
                    {
                        this.estadosAP1.push(aux);
                    }
                    this.estadoAP1.label=this.estadoAP1.id;
                    if(this.estadosAP1.length===1)
                    {
                        if(!this.estadosDistintos(this.estadosAP2,this.estadoAP1))
                        {
                            swal("El id debe ser distinto al/los estado(s) del otro autómata",{
                                className: "alertas",
                                button: "Aceptar",
                                icon: "warning",
                                title: "Aviso",
                            });
                            return;
                        }
                        this.estadosAP1.push(this.estadoAP1);
                        this.transicionAP1.from='inicio';
                        this.transicionAP1.label='';
                        this.transicionAP1.to= this.estadoAP1.id;
                        console.log("tr1", this.transicionAP1);
                        this.transicionesAP1.push(this.transicionAP1);
                        this.transicionAP1= {from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
                        this.estadoAP1= {id:'', label:'',color:'#C52C0B' ,final:false};
                        this.drawAutomata();
                        console.log("tr2",this.transicionesAP1);
                        return;
                    }
                    else{
                        if(!this.estadosDistintos(this.estadoAP2,this.estadoAP1))
                        {
                            swal("El id debe ser distinto al/los estado(s) del otro autómata",{
                                className:"alertas",
                                button:"Aceptar",
                                icon:"warning",
                                title:"Aviso",
                            });
                            return;
                        }
                        this.estadosAP1.push(this.estadoAP1);
                        this.estadoAP1= {id:'', label:'',color:'#C52C0B' ,final:false};
                        this.drawAutomata();
                        return;
                    }
                }
                else{
                    if(this.apSeleccionado===2)
                    {
                         if(this.estadoAP2.id==='')
                        {
                            swal("Por favor, ingrese un id",{
                                className: "alertas",
                                button: "Aceptar",
                                icon: "warning",
                                title: "Aviso",
                            });
                            return;
                        }
                        if(this.existeEstado(this.estadosAP2,this.estadoAP2))
                        {
                            swal("El estado ya existe. Ingrese un estado con otro id.",{
                                className: "alertas",
                                button: "Aceptar",
                                icon: "warning",
                                title: "Aviso",
                            });
                            return;
                        }
                        if(this.estadosAP2.length===0)
                        {
                            this.estadosAP2.push(aux);
                        }
                        this.estadoAP2.label=this.estadoAP2.id;
                        if(this.estadosAP2.length===1)
                        {
                            if(!this.estadosDistintos(this.estadosAP1,this.estadoAP2))
                            {
                                swal("El id debe ser distinto al/los estado(s) del otro autómata",{
                                    className: "alertas",
                                    button: "Aceptar",
                                    icon: "warning",
                                    title: "Aviso",
                                });
                                return;
                            }
                            this.estadosAP2.push(this.estadoAP2);
                            this.transicionAP2.from='inicio';
                            this.transicionAP2.label='';
                            this.transicionAP2.to= this.estadoAP2.id;
                            this.transicionesAP2.push(this.transicionAP2);
                            this.transicionAP2= {from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
                            this.estadoAP2= {id:'', label:'',color:'#C52C0B' ,final:false};
                            this.drawAutomata();
                            return;
                        }
                        else{
                            if(!this.estadosDistintos(this.estadoAP1,this.estadoAP2))
                            {
                                swal("El id debe ser distinto al/los estado(s) del otro autómata",{
                                    className:"alertas",
                                    button:"Aceptar",
                                    icon:"warning",
                                    title:"Aviso",
                                });
                                return;
                            }
                            this.estadosAP2.push(this.estadoAP2);
                            this.estadoAP2= {id:'', label:'',color:'#C52C0B' ,final:false};
                            this.drawAutomata();
                            return;
                        }
                    }
                }
            }        
        },

        existeEstado(estados,estado)
        {
            for(var i=0; i<estados.length; i++)
            {
                if(estados[i].id==estado.id)
                {
                    return true;
                }
            }
            return false;
        },

        existeFinal(estados){
            for(var i=0; i<estados.length;i++)
            {
                if(estados[i].final===true)
                {
                    return true;
                }
            }
            return false;
        },

        marcarFinal(id){
            if(this.option===1)
            {
                for(var i=0; i<this.estadosAutomataAFD.length; i++)
                {
                    if(this.estadosAutomataAFD[i].id===id && this.estadosAutomataAFD[i].final===false)
                    {
                        this.estadosAutomataAFD[i].final= true;
                        this.estadosAutomataAFD[i].shape= 'diamond';
                        this.estadosAutomataAFD[i].color = '#5cb85c';
                        this.drawAutomata();
                        console.log("Estado final: ", i, this.estadosAutomataAFD[i].final);
                    }
                    else{
                        if(this.estadosAutomataAFD[i].id===id && this.estadosAutomataAFD[i].final===true)
                        {
                            this.estadosAutomataAFD[i].final= false;
                            this.estadosAutomataAFD[i].shape= 'ellipse';
                            this.estadosAutomataAFD[i].color= '#C52C0B';
                            this.drawAutomata();
                        }
                    }
                }
            }
            else{
                if(this.apSeleccionado===1)
                {
                    for(var j=0; j<this.estadosAP1.length; j++)
                    {
                        if(this.estadosAP1[j].id===id && this.estadosAP1[j].final===false)
                        {
                            this.estadosAP1[j].final= true;
                            this.estadosAP1[j].shape= 'diamond';
                            this.estadosAP1[j].color = '#5cb85c';
                            this.drawAutomata();
                            console.log("Estado final: ", i, this.estadosAP1[j].final);

                        }
                        else
                        {
                            if(this.estadosAP1[j].id===id && this.estadosAP1[j].final===true)
                            {
                                this.estadosAP1[j].final= false;
                                this.estadosAP1[j].shape= 'ellipse';
                                this.estadosAP1[j].color = '#C52C0B';
                                this.drawAutomata();
                                console.log("Estado final: ", i, this.estadosAP1[j].final);
                            }
                        }
                    }
                }
                else{
                    if(this.apSeleccionado===2)
                    {
                        for(var k=0; j<this.estadosAP2.length; k++)
                        {
                            if(this.estadosAP2[k].id===id && this.estadosAP2[k].final===false)
                            {
                                this.estadosAP2[k].final= true;
                                this.estadosAP2[k].shape= 'diamond';
                                this.estadosAP2[k].color = '#5cb85c';
                                this.drawAutomata();
                                console.log("Estado final: ", i, this.estadosAP2[k].final);

                            }
                            else
                            {
                                if(this.estadosAP2[k].id===id && this.estadosAP2[k].final===true)
                                {
                                    this.estadosAP2[k].final= false;
                                    this.estadosAP2[k].shape= 'ellipse';
                                    this.estadosAP2[k].color = '#C52C0B';
                                    this.drawAutomata();
                                    console.log("Estado final: ", i, this.estadosAP2[k].final);
                                }
                            }
                        }

                    }
                }
            }
        },

        existeCaracterAFD(caracter){
            for(var i=0; i<this.alfabetoAFD.length;i++)
            {
                if(this.alfabetoAFD[i]===caracter)
                {
                    return true;
                }
            }
            return false;
        },

        analizarCadenaAFD(){
            var word=this.cadena.split('');
            var transicionesEstadoActual=[];
            var estadoActual;
            console.log(word);
            if(this.estadosAutomataAFD.length===1 || this.estadosAutomataAFD.length===0)
            {
                swal("Debe ingresar el automata antes de analizar la palabra",{
                    className: "alertas",
                    button: "Aceptar",
                    title: "Aviso",
                    icon: "warning",
                });
                return;
            }
            else{
                if(!this.existeFinal(this.estadosAutomataAFD))
                {
                    swal("Para analizar la palabra debe marcar como final a lo menos un estado en el autómata",{
                        className: "alertas",
                        button: "Aceptar",
                        title: "Aviso",
                        icon: "warning",
                    });
                    return;
                }
            }
            estadoActual=this.estadosAutomataAFD[1].id;
            console.log(estadoActual);
            for(var i=0; i<word.length;i++)
            {
                if(!this.existeCaracterAFD(word[i]))
                {
                    swal("La palabra no pertenece al lenguaje",{
                        className: "alertas",
                        button: "Aceptar",
                        title: "Resultado del análisis",
                        icon: "error",
                    });
                    return;
                }
                for(var j=0; j<this.transicionesAutomataAFD.length;j++)
                {
                    if(this.transicionesAutomataAFD[j].from===estadoActual){
                        transicionesEstadoActual.push(this.transicionesAutomataAFD[j]);
                    }
                }
                for(var k =0; k<transicionesEstadoActual.length; k++)
                {
                    if(transicionesEstadoActual[k].label===word[i])
                    {
                        estadoActual=transicionesEstadoActual[k].to;
                        console.log("Estado Actual: ", estadoActual);
                    }
                }
                transicionesEstadoActual=[];
            }

            for(var t=0; t<this.estadosAutomataAFD.length; t++)
            {
                if(estadoActual===this.estadosAutomataAFD[t].id)
                {
                    if(this.estadosAutomataAFD[t].final===true)
                    {
                        swal("La palabra pertenece al leguaje",{
                            className: "alertas",
                            button: "Aceptar",
                            title: "Resultado del análisis",   
                        });
                        return;
                    }
                    else{
                        swal("La palabra no pertenece al lenguaje",{
                            className: "alertas",
                            button: "Aceptar",
                            title: "Resultado del análisis",
                            icon: "error",
                        });
                        return;
                    }
                }
            }
            
        },

        drawAutomata(){
            var afd= document.getElementById("AFD");
            var ap1= document.getElementById("AP1");
            var ap2= document.getElementById("AP2");
            var apConcatenados= document.getElementById("APCONCATENADO");
            var apUnidos= document.getElementById("APUNIDOS");

            var dataAFD= {
                nodes: this.estadosAutomataAFD,
                edges: this.transicionesAutomataAFD,
            };

            var dataAP1= {
                nodes: this.estadosAP1,
                edges: this.transicionesAP1,
            };

            var dataAP2= {
                nodes: this.estadosAP2,
                edges: this.transicionesAP2,
            };

            var dataAPConcatenados= {
                nodes: this.estadosAutomataConcatenacionAP,
                edges: this.transicionesAutomataConcatenacionAP,
            };

            var dataAPUnidos= {
                nodes: this.estadosAutomataUnionAP,
                edges: this.transicionesAutomataUnionAP,
            };


            var options = {
                height: 320 +'px',
                edges:{
                    arrows: 'to',
                },
            };

            if(this.option===1)
            {
                var networkAFD= new vis.Network(afd,dataAFD,options);
            }

            if(this.option===2)
            {
                var networkAP1= new vis.Network(ap1,dataAP1,options);
                var networkAP2= new vis.Network(ap2,dataAP2,options);
            }

            if(this.opcion===3)
            {
                var networkUnion= new vis.Network(apUnidos,dataAPUnidos,options);//el Apus nahasapeemapetilon
            }

        },

        encontrarExpresionRegular(){
            var finales=[];

            //Se busca los finales y se agregan al arreglo finales
            for(var i=0; i<this.estadosAutomataAFD.length; i++)
            {
                if(this.estadosAutomataAFD[i].final===true)
                {
                    finales.push(this.estadosAutomataAFD[i].id);
                }
            }

            //Se busca si hay transiciones que salen de los finales. Si ese es el caso, se procede a crear un nuevo estado final y los antiguos dejan de ser finales.
            if(this.salenFinales(finales)){
                //Se crean las transiciones desde los antiguos finales al nuevo final con una transicion vacía.
                for(var j=0; j<finales.length;j++)
                {
                    this.transicionAutomataAFD.from=finales[j];
                    this.transicionAutomataAFD.to='Final';
                    this.transicionAutomataAFD.label='E';
                    this.transicionesAutomataAFD.push(this.transicionAutomataAFD);
                    this.transicionAutomataAFD={from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}};
                }
            }
            console.log("Estados:",this.estadosAutomataAFD);

            //Buscar intermedio entre el inicial (q0) y q2 
            var primero='inicio';   //INICIO   -  INTERMEDIO   -   Q1 Q2 ...
            var intermedio={from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}};
            var revisado=[];
            var transicion={from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}};
            var transaux=[];
            for(var k=0; k<this.transicionesAutomataAFD.length;k++)
            {
                console.log("k =", k, "/ ", this.transicionesAutomataAFD.length);
                if(this.transicionesAutomataAFD[k].from===primero)
                {
                    intermedio=this.transicionesAutomataAFD[k];
                    console.log("Intermedio: ", intermedio.to);
                    console.log("Revisados: ", revisado);
                    for(var t=0; t<this.transicionesAutomataAFD.length;t++)
                    {
                        console.log("t =", t, "/ ", this.transicionesAutomataAFD.length);
                        if(this.transicionesAutomataAFD[t].from===intermedio.to && t!=k)
                        {
                            console.log("encontro to del revisando en el from del transiciones");
                            transicion.from=primero;
                            if(this.transicionesAutomataAFD[t].from==this.transicionesAutomataAFD[t].to)
                            {
                                console.log("entro 3.1");
                                if(this.transicionesAutomataAFD[t].label.includes('+'))
                                {
                                    transicion.label=transicion.label+'('+this.transicionesAutomataAFD[t].label+')*';
                                }
                                else{
                                    transicion.label=transicion.label+this.transicionesAutomataAFD[t].label+'*';
                                }
                            }
                            else{
                                console.log("entro 3.2");
                                transicion.label=transicion.label+this.transicionesAutomataAFD[t].label;
                            }
                            transicion.to=this.transicionesAutomataAFD[t].to;
                            console.log("transicion push", transicion);
                            this.transicionesAutomataAFD.push(transicion);
                            transicion={from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}};
                            console.log("splice", this.transicionesAutomataAFD[t].from,this.transicionesAutomataAFD[t].label, this.transicionesAutomataAFD[t].to);
                            this.transicionesAutomataAFD.splice(t,1);
                            if(k!=0){
                                k--;
                            }
                            if(t!=0){
                                t--;
                            }
                                
                            
                            for(let p=0; p<this.transicionesAutomataAFD.length; p++){
                                for(let q=1; q<this.transicionesAutomataAFD.length; q++){
                                    console.log("------------------");
                                    if(p!=q){
                                        if(this.transicionesAutomataAFD[p].from===this.transicionesAutomataAFD[q].from && this.transicionesAutomataAFD[p].to===this.transicionesAutomataAFD[q].to){
                                            this.transicionesAutomataAFD[p].label=this.transicionesAutomataAFD[p].label.concat(this.transicionesAutomataAFD[q].label);
                                            console.log("splice del concat", this.transicionesAutomataAFD[q].from,this.transicionesAutomataAFD[q].label, this.transicionesAutomataAFD[q].to);
                                            this.transicionesAutomataAFD.splice(q,1);
                                            p--;
                                            q--;
                                        }
                                    }
                                }
                            }
                            
                        }
                    }
                    revisado.push(intermedio.to);
                }
                
            }
            this.drawAutomata();



        },

        salenFinales(finales){
            console.log("funcion salen finales");
            for(var j=0; j<this.transicionesAutomataAFD.length;j++)
            {
                for(var k=0; k<finales.length;k++)
                {
                    if(this.transicionesAutomataAFD[j].from===finales[k])
                    {
                        for(var t=0; t<this.estadosAutomataAFD.length;t++){
                            if(this.estadosAutomataAFD[t].final===true){
                                this.estadosAutomataAFD[t].final=false;
                                this.estadosAutomataAFD[t].shape='ellipse';
                                this.estadosAutomataAFD[t].color='#C25C0B';
                            }
                        }
                        this.estadoAutomataAFD.final=true;
                        this.estadoAutomataAFD.shape='diamond';
                        this.estadoAutomataAFD.color='#5cb85c';
                        this.estadoAutomataAFD.id='Final';
                        this.estadoAutomataAFD.label='Final';
                        this.estadosAutomataAFD.push(this.estadoAutomataAFD);
                        this.estadoAutomataAFD={id: '', label: '', color: '#C25C0B', final: false};
                        return true;
                    }
                }
            }
            return false;
        },

        sonIguales(final,cadena){                     
            var Final=final.split('E');    //EbabE -> split(E) ==> ["","bab",""]
            var cad= cadena.split('E');    // Ebabaa -> split(E) ==> ["","babaa"]
            var aux1;
            var aux2;
            for(var i=0; i<Final.length;i++)
            {
                if(Final[i]!='')
                {
                    aux1=Final[i];           //aux1="bab"
                }
            }   
            aux1=aux1.split('');             //aux1= ['b','a','b']
            for(var j=0; j<cad.length;j++)   
            {
                if(cad[j]!='')
                {
                    aux2=cad[j];             //aux2="babaa"
                }
            }
            aux2=aux2.split('');             //aux2=['b','a','b','a','a']

            if(aux2.length>=aux1.length)        //aca los recorre y compara 
            {
                for(k=0; k<aux1.length;k++)
                {
                    if(aux2[k]!=aux1[k])
                    {
                        return false;
                    }
                }
                return true;
            }
            else{
                return false;
            }
                  
        },


    }
}
</script>