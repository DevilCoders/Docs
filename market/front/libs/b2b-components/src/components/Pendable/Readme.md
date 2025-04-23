Компонент для отрисовки лэйера и спиннера во время обновления контента.
Лэйер и спиннер автоматически позиционируются относительно размеров контента и скролла.

```jsx
initialState = {isPending: false, count: 1};
toggle = () => setState(({isPending}) => ({isPending: !isPending}));
inc = () => setState(({count}) => ({count: count + 1}));
reset = () => setState({count: 1})


const __html = `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec suscipit scelerisque ligula ut laoreet. Pellentesque eu metus quis metus tristique venenatis ac ac justo. Nam aliquet, erat iaculis sodales finibus, elit quam egestas justo, non ultrices ligula urna non ante. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Duis pretium cursus orci nec tempor. Morbi vestibulum tempus placerat. Nullam id urna viverra, mattis dui sit amet, pretium ligula. Vestibulum pretium ullamcorper sollicitudin. Mauris non sem ac ex lobortis volutpat at vitae sapien. Mauris auctor nulla et ultricies gravida.

<br /><br />

Curabitur sodales leo velit, a varius urna commodo ut. Aliquam nec nisl nulla. Pellentesque pellentesque felis ante, in pellentesque risus gravida non. Nunc in velit ipsum. Duis rhoncus, orci pretium feugiat maximus, erat turpis rutrum urna, nec eleifend arcu velit a nisi. Vivamus pretium porttitor ipsum, at aliquet ex. Vivamus non erat orci. Donec at dapibus lacus, sit amet faucibus nibh. Aliquam hendrerit bibendum eros. Mauris rutrum nec turpis nec interdum. Suspendisse bibendum sem at venenatis varius. Vestibulum luctus lacus vel ipsum ultricies viverra. Sed diam quam, tincidunt ac egestas eget, convallis porttitor nunc. Suspendisse bibendum euismod iaculis. Vestibulum ut egestas eros, a ultrices sapien.

<br /><br />

Quisque sodales libero dapibus sagittis imperdiet. Vivamus dui ante, tincidunt at leo id, posuere finibus dui. Maecenas eget condimentum nisi, at commodo eros. Etiam imperdiet faucibus elit, in tincidunt ipsum scelerisque ac. Donec luctus arcu eu lorem hendrerit gravida. Nulla laoreet volutpat orci, ut rhoncus nulla aliquet ut. Quisque tincidunt dolor in mollis pharetra. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Donec ut varius nulla, non posuere ipsum. Nunc laoreet lectus purus, sed porta elit posuere nec. Nunc pulvinar mi in urna laoreet, vitae euismod ante tincidunt. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae;

<br /><br />

Ut gravida enim erat. Quisque ut tempus arcu, ac faucibus mauris. Fusce efficitur massa id ante varius ultrices. Suspendisse potenti. Etiam nec pharetra dolor, id dapibus velit. Nullam tempor nec quam et finibus. Vestibulum ut viverra tellus. Sed vehicula dolor vitae pharetra tincidunt. Etiam id suscipit augue. Donec felis sapien, pretium at ex vitae, tempor laoreet mauris. Aenean vulputate libero sed iaculis blandit. Vivamus quis consectetur elit. Vestibulum porttitor nibh risus, et facilisis ipsum pretium auctor. Etiam pellentesque ante vel ante lobortis suscipit. Fusce dapibus auctor sapien a facilisis. Mauris maximus turpis id risus luctus, vestibulum tristique orci consectetur.

<br /><br />

Sed dignissim faucibus enim, eu vehicula tortor pretium non. Sed semper lectus non tristique viverra. Suspendisse tincidunt porta felis. Praesent tristique imperdiet efficitur. Maecenas posuere commodo finibus. Sed tempus metus vel elit finibus, non volutpat lectus dictum. Maecenas bibendum, orci a facilisis ornare, urna nunc maximus lacus, quis vehicula risus purus vel leo.
`;

<section>
    <Filters>
        <Button onClick={toggle}>{!state.isPending ? 'Старт' : 'Стоп'}</Button>
        <Button onClick={inc}>Больше текста!</Button>
        <Button onClick={reset}>Резет</Button>
    </Filters>

    <Pendable pending={state.isPending}>
        <Text>
            {[...Array(state.count)].fill(<span dangerouslySetInnerHTML={{__html}} />)}
        </Text>
    </Pendable>
</section>
```
