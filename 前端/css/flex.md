### Flex 布局的相关属性
|属性|值|描述|
|--|--|--|
|display|flex，inline-flex|设置该元素为Flex容器,设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。|
|flex-direction|row ;row-reverse ;column ;column-reverse|容器的主轴方向|
|flex-wrap|nowrap ;wrap ; wrap-reverse|容器元素的换行，换行样式|
|flex-flow| <flex-direction>  <flex-wrap>;  |flex-direction属性和flex-wrap属性的简写形式|
|justify-content|flex-start ; flex-end ;center ;space-between; space-around; |项目在主轴上的对齐方式|
|align-items|flex-start ;flex-end ;center ;baseline ; stretch  |容器元素对于交叉轴的对齐方式|
|align-content|flex-start ; flex-end ; center ; space-between ; space-around ; stretch|align-content属性定义了多根轴线的对齐方式|


### 容器内部项目的属性
|属性|值|描述|
|--|--|--|
|order|0,1,2 ...| 越小越靠前|
|flex-grow|整数|item放大比例|
|flex-shrink|整数|item的缩小比例|
|flex-basis| <length>;auto|项目在分配多余空间前占据的大小|
|flex|none ; [ <'flex-grow'> <'flex-shrink'>? ;; <'flex-basis'> ] |flex属性是flex-grow, flex-shrink 和 flex-basis的简写|
|align-self|auto ; flex-start ; flex-end ; center ; baseline ;stretch;|项目自己的独特的对齐方式|