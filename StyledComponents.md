# Styled Components

## Grid-Area
 ```html
 <Grid
        gridGap="20px"
        gridTemplateAreas={`
          'header header header'
          'left middle right'
          'footer footer footer'`}
        gridTemplateColumns="100px auto 100px"
        gridTemplateRows="50px auto 50px"
      >
        <Div backgroundColor="white" gridArea="header">
          Hello
        </Div>
        <Div backgroundColor="red" gridArea="left">
          Hello
        </Div>
        <Div backgroundColor="black" gridArea="middle">
          Hello
        </Div>
        <Div backgroundColor="blue" gridArea="right">
          Hello
        </Div>
        <Div backgroundColor="pink" gridArea="footer">
          Footer
        </Div>
 </Grid>
 ```
