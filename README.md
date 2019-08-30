<img src="/src/images/CSS_logo_2019_darkblue_no border_v08.svg" width="200px">

# controlsystemstudio.org [![Netlify Status](https://api.netlify.com/api/v1/badges/8f0d3cc9-2b0b-48ea-82ac-172247bf3480/deploy-status)](https://app.netlify.com/sites/lucid-clarke-a55e88/deploys)

Redesign of the website for Control System Studio (CS-Studio). Made using GatsbyJS and hosted on netlify. 

https://lucid-clarke-a55e88.netlify.com/

## Developing/Testing locally
Gatsby has a fantastic development server feature, which allows you to preview the page immediately without building it. Make sure to install all npm dependencies using `npm install` the first time you run the site.
    
    $ npm start
  
## Building
To run the site on a server, it needs to be built first.

    $ npm install
    $ npm run build
  
The website files can be found in `public`.

## Editing content
The pages can be found in the folder `src/pages`, whereas resuable parts can be found in `src/components` as React components.
Pages are written in the JSX format, which is similar to HTML, but behaves differently in certain usecases.
Simple paragraphs and lists can be written in the familiar HTML format, but for example images are embedded in a different way.
Images are placed inside `src/images` and queried using GraphQL.
    
    opi: file(
        relativePath: { eq: "CS-Studio-OPIs_and_Keyvisual_v03_big.png" }
      ) {
        childImageSharp {
          fluid(maxWidth: 3840, maxHeight: 2160) {
            ...GatsbyImageSharpFluid_withWebp
          }
        }
      }
      
When running the development server, you can go to [localhost:8000/__graphql](http://localhost:8000/__graphql) to test out GraphQL queries.

This query is included inside of the useStaticQuery hook inside of the main component of the page like this:
    
    // First import the relevant functions and components
    import { graphql, useStaticQuery } from 'gatsby'
    import Img from 'gatsby-images'
    
    // Then query inside the main component
    const Component = () => {
        const images = useStaticQuery(graphql`
            query {
                // <- image query here
            }
        `)
        
        return (
            // ...
        )
    }
    
The image can then be displayed using gatsby-images' `Img` component.

    <Img
          fluid={images.opi.childImageSharp.fluid}
    />

For more detail please refer to the [Gatsby documentation](https://www.gatsbyjs.org/docs/working-with-images/).

## Downloads
Because links to downloads can be updated quite frequently, they are separated from the Download page to make editing them a little easier. You can find the file where you can define each link necessary in `src/utils/downloadinfo.js`
