<template>
    <div class="container mt-5 pt-4">
        <h1 class="fredoka textocolor my-2">Tipos de autómatas con los que se trabajará en esta aplicación web:</h1>
        <div class="row bg-white rounded shadow mt-4 cardaux">
            <div class="col-12 cardaux">
                <div class="row d-flex justify-content-center mx-2 my-2 pt-2">
                    <h4 class="textocolor fredoka my-2">Tipos de Autómatas</h4>
                </div>
                <hr>
                <div class="row accordion" id="automatas">
                    <ul class="col-lg-3 col-sm-12 my-2 list-group list-group-flush">
                        <li class="list-group-item analisis collapsed info textocolor" data-toggle="collapse" data-target="#af" aria-expanded="false" aria-controls="af">
                            Autómata de Pila (AP)
                        </li>
                        <li class="list-group-item analisis collapsed info textocolor" data-toggle="collapse" data-target="#afd" aria-expanded="false" aria-controls="afd">
                            Expresión Regular (ER)
                        </li>
                        
                    </ul>
                    <div class="col-lg-7 col-sm--12 my-2">
                        <div class="collapse" id="af" data-parent="#automatas">
                            <div class="my-3">
                                <div class="row d-flex justify-content-center">
                                    <h4 class="textocolor fredoka">Autómata De Pila</h4>
                                </div>
                                <p class="textocolor lato" >
                                    Existe un tipo de autómata que define los lenguajes independientes del contexto.
                                    Dicho autómata, conocido como “autómata de pila”, es una extensión del autómata finito
                                    no determinista con transiciones-ε ,
                                    el cual constituye una forma de definir los lenguajes regulares.
                                    El autómata de pila es fundamentalmente un AFN-ε con la adición de una pila.
                                    <br>
                                    <br>
                                    Un autómata con pila puede ser descrito como una séptupla <strong><em>M = (S,Σ,Γ,δ,s,Z,F)</em></strong>&nbsp; donde: <br>
                                    <strong>S</strong>&nbsp;es un conjunto finito de estados <br>
                                    <strong>Σ</strong> y <strong>Γ</strong>&nbsp; son alfabetos (símbolos de entrada y de la pila respectivamente) <br>
                                    <strong>δ : S × (Σ &cup; {ε}) x Γ &rarr; &weierp;(S x Γ*) </strong><br>
                                    <strong>s &isin; S</strong>&nbsp; es el estado inicial <br>
                                    <strong>Z &isin; Γ</strong>&nbsp; es el símbolo inicial de la pila<br>
                                    <strong><em>F &sube; S</em></strong>&nbsp; es un conjunto de estados de aceptación o finales<br>
                                </p>
                                <div class="row justify-content-center">
                                    <div class="image-parent">
                                        <img src="https://upload.wikimedia.org/wikipedia/commons/1/13/Ejemplo_1_AFPN.JPG"  alt="AP" style="border-radius:10px;">
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="collapse" id="afd" data-parent="#automatas">
                            <div class>
                                <div class="row d-flex justify-content-center">
                                    <h4 class="textocolor fredoka">Expresión Regular</h4>
                                </div>
                                <p class="textocolor lato" >
                                   Una Expresión regular es un generador de lenguajes sobre un alfabeto con ciertas caractericticas (restricciones).
                                   En otras palabras, una expresión regular es una forma de representar los lenguajes regulares. <br>
                                   Ésta se construye utilizando los caracteres del alfabeto sobre el cual se define el lenguaje.
                                </p>
                                <div class="row justify-content-center">
                                    <div class="image-parent">
                                        
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        
                    </div>
                </div>               
            </div>
        </div>          
        
    </div>
    
</template>