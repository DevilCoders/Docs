### Playground

```jsx
import DotsPager from '@self/root/src/components/DotsPager';

const styles = {
    dotsPager: {
        position: 'relative',
        bottom: '-16px',
    },

    wrapper: {
        display: 'flex',
        justifyContent: 'center',
    },

    root: {
        paddingBottom: '16px',
    },
}

const renderDots = ({currentSlide, slideCount, goToSlide}) => (
    <div style={styles.dotsPager}>
        <DotsPager
            index={currentSlide}
            pages={slideCount}
            onClick={goToSlide}
        />
    </div>
);


setTimeout(() => {
    // Нужно для того, чтобы проинитилась карусель после изменения параметров
    window.dispatchEvent(new Event('resize'));
});

<div style={styles.root}>
    <NukaCarousel
        autoplay={false}
        wrapAround={false}
        dragging={true}
        renderCenterLeftControls={null}
        renderCenterRightControls={null}
        renderBottomCenterControls={renderDots}
    >
        <div style={styles.wrapper} >
            <img src={helper.generateImage({w: 350, h: 300, text: 'slide1'})} />
        </div>
        <div style={styles.wrapper} >
            <img src={helper.generateImage({w: 350, h: 200, text: 'slide2'})} />
        </div>
        <div style={styles.wrapper} >
            <img src={helper.generateImage({w: 200, h: 200, text: 'slide3'})} />
        </div>
        <div style={styles.wrapper} >
            <img src={helper.generateImage({w: 200, h: 250, text: 'slide4'})} />
        </div>
        <div style={styles.wrapper} >
            <img src={helper.generateImage({w: 350, h: 150, text: 'slide5'})} />
        </div>
    </NukaCarousel>
</div>
```
