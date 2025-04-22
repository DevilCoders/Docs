Баджи для AppStore

```jsx harmony
const Grid = require('../../styleguide/components/grid/Grid').default;

<React.Fragment>
    <Grid container spacing={2} style={{width: 900}}>
        {['l', 'm', 's'].map(size => (
            <>
                <Grid key={`${size}-title`} item spacing={1} size={12}><h3>Размер {size}</h3></Grid>
                {
                    ['ru', 'en', 'ro', 'lv', 'az', 'fr', 'he', 'NO'].map(lang => (
                        <> 
                            <Grid key={`${lang}${size}-title`} item spacing={1} size={3} style={{textAlign: 'right'}}><strong>{lang}</strong></Grid>
                            {
                                ['ios', 'android', 'huawei'].map(platform => (
                                    <Grid key={`${platform}${lang}${size}`} item spacing={1} size={3} title={lang}>
                                        <AppstoreBadge platform={platform} lang={lang} size={size}/>
                                    </Grid>
                                ))
                            }
                        </>
                    ))
                }
            </>
        ))}
    </Grid>
</React.Fragment>;
```
