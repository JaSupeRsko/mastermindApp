<template>
    <button :disabled="block" :class="{'btn': true, 'btn-marked': isMarked, 'btn-miss': isMiss, 'btn-dead': isDead, 'btn-hit': isHit }" v-on:click="click()">{{ element.x + element.y }}</button>
</template>

<script>
import { v4 } from 'uuid';

    export default {
        data: function () {
            return {
                identifier: v4(),
                isMarked: false,
            };
        },
        props: {
            element: null,
            block: null,
            isMiss: null,
            isHit: null,
            isDead: null,

            myPickedNodes: null,
            curShipLen: null,
            markedFields: null,
            allMarkedFields: null,
            rotation: null,
        },
        mounted () {
            console.log('Mounted!');
            if (this.element.isMarked)
                this.isMarked = true;
        },
        methods: {
            showLog: function (text) {
                var message = 'Klik: ';
                console.log(message + text);
            },
            click: function () {

                //this.isMarked = !this.isMarked;
                console.log("click");
                var check = true;
                switch (this.rotation){
                    case 0:
                        for(var j=0;j<this.curShipLen;j+=1)
                        {
                            if(this.element.x+j<10)
                            {
                                this.allMarkedFields.forEach(ship => {
                                    ship.forEach(node =>{
                                        if(this.element.x+j==node.x && this.element.y==node.y){
                                            check=false;
                                        }
                                    })
                                });
                            }
                        }
                        if(check){
                            for(var i=0;i<this.curShipLen;i+=1)
                            {
                                this.isMarked=true; //emitowanie do innych elementow zeby sie marknely

                                this.$emit('elementClick', {
                                x: this.element.x,
                                y: this.element.y,
                                marked: this.isMarked,
                                });
                            }
                        }
                        break;
                    case 1:
                        
                        break;
                    case 2:
                        
                        break;
                    case 3:
                        
                        break;
                }
                // console.log(this.element.x);
                // hey elementClick happened with element
                
            },
        },
    }
</script>

<style>
    .btn {
        max-width: 100%;
        max-height: 100%;
        border: 1px solid black;
        margin: 1px;
        aspect-ratio: 1 / 1;
        padding: 0 0;
    }

    .btn-marked {
        background-color: deepskyblue;
    }
    
    .btn-miss {
        background-color: gray;
    }

    .btn-hit {
        background-color: red;
    }

    .btn-dead {
        background-color: black;
    }
</style>