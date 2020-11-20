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
                        <form @submit.prevent="">
                            <div class="form-group">
                                <label>Ingrese la palabra: </label>
                                <input type="text" class="form-control">
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
                                <input type="text" minlength="1" class="form-control" v-model="transicionAP1.label">
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
                        <div class="mb-3" id="AP1" style="border:1px solid lightgray;"></div>
                    </div>
                    <div class="col-md-6" v-if="option===2">
                        <h4 class="text-center fredoka my-3">Autómata de Pila 2</h4>
                        <div class="mb-3" id="AP2" style="border:1px solid lightgray;"></div>
                    </div>
                </div>
            </div>

            <!--REPRESENTACION AUTOMATAS-->

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
                            <tr>
                                <td>a</td>
                                <td>a</td>
                                <td>a</td>
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

            estadosAP2:[{id: 'inicio', label: 'inicio', color:'#75616b47', final: false}],
            estadoAP2:{id: '', label: '', color: '#C25C0B', final: false},
            transicionesAP2:[],
            transicionAP2:{from: '', label: '', to: '', color: {color: 'rgb(0,0,0)'}},
            //transicion automata pila = {caracter que consume, caracter que elimina, caracter que ingresa}
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
                this.addCaracterToAlfabeto();
                this.transicionesAutomataAFD.push(this.transicionAutomataAFD);
                this.transicionAutomataAFD={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}}; 
            }
            else{
                if(this.apSeleccionado===1)
                {
                    if(this.transicionAP1.from ==='' || this.transicionAP1.to ==='')
                    {
                        swal("Estados no ingresadow. Rellene todos los campos antes de continuar",{
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
                    this.addCaracterToAlfabeto();
                    this.transicionesAutomataAFD.push(this.transicionAP1);
                    this.transicionAP1={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
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
                        this.transicionAP2={from:'',label: '',to:'',color:{color:'rgb(0,0,0)'}};
                    }
                }
            }
            this.drawAutomata();
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
                    this.transicionAutomataAFD.label='';
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

        },


    }
}
</script>