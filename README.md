# tnc-toolkit

TNC-Toolkit is a TNC-Toolkit is a tool for querying MapBiomas collections that, based on a polygon geometry, allows recovering information on transitions over time from a series of land use and land cover maps. These transition layers are added to the map and are shown as years in which these changes occur from natural vegetation (mainly Forest) to anthropic class (agriculture or pasture).

## Google Earth Engine Repository

    https://code.earthengine.google.com/?accept_repo=users/geosimplear/tnc-toolkit

1. Add the repository in Code Editor interface ([Open Repository](https://code.earthengine.google.com/?accept_repo=users/geosimplear/tnc-toolkit)). 
![repository](images/add-repo.png)

2. Run the toolkit open the [app.js](https://code.earthengine.google.com/?scriptPath=users%2Fgeosimplear%2Ftnc-toolkit%3Aapp.js) script from [Code Editor](https://code.earthengine.google.com/) and run it from Run.

## Interface

![toolkit-interfaz](images/toolkit-EN.png)

 1. Target geometry options.
 2. Run analysis button.
 3. Changed years legend
 4. LULC MapBiomas Legend
 5. Report area
 6. Area transitions plot
 7. Areas corresponding to the forest law regulations (OTBN)
 8. Layers included in the map
 9. Target geometry visualization

### Interface language

The toolkit can be used in different languages, currently it can be used in English [EN] or Spanish [ES] indicating this in section 1) Language of the app.js script.

```Javascript
// 1) Laguage Setting
var language = "ES";
```
It is possible to incorporate other languages from the [i18n.js](https://code.earthengine.google.com/?scriptPath=users%2Fgeosimplear%2Ftnc-toolkit%3Amodules%2Fi18n.js) module.

## Target geometry options

There are two options for entering a target geometry for analysis. The first is by drawing it on the map and the second is by selecting it from an asset available in GEE to which we have access.

The second option can be set in the app.js configuration in section 2 assets settings. The AOI section allows you to define different layers to use as analysis geometries.

```Javascript
// 2) Assets Settings
var assets = {
    // AOI Targets from assets
    aoi: [
        {
            label: "Ejemplo", 
            path: "users/geosimplear/tnc/parcelas-ejemplo", 
            field: "system:index"
        }
        
    ],
    // Query data assets
    datasets: {
        // MapBiomas Collections Settings
        cover: {
            label: "MapBiomas Chaco (v4.1)",
            path: "projects/mapbiomas-chaco/public/collection4/mapbiomas_chaco_collection4_1_integration_v1",
            style: {min:0, max: 65, bands: ["classification_2022"] ,palette: palettes.get('atlantic_forest')}
        },
        // Boundaries categories forest law  (Referencia)
        otbn:{
            label: "OTBN",
            path: "projects/geosimple-ipcva/assets/OTBN-250m-mask1",
            style: {}
        },
        // Administrative limits
        provincia:{
          label: "Provincias",
          path: "users/geosimplear/tnc/provincia",
          style: {},
          field: "nam"
        },
        // Administrative limits
        departamento:{
            label: "Provincias",
            path: "users/geosimplear/tnc/departamento",
            style: {},
            field: "nam"
          }
    }
}
```

## Years of change legend

Legend showing the years that show changes from forest to agriculture or pasture classes.

### LULC MapBiomas Legend

MapBiomas legend of the current collection

## Report area

Report area, all the information recovered from the AOI is shown in the report. It includes information on the location (province and department), AOI area and area of change in hectares and two analysis graphs. One on the area of change per year and another on the area in relation to the OTBN regulations.

## Area transitions plot

This graph shows the areas of transitions by year. These transitions can be edited in app.js in section 3) Target Analysis. Each bar in the graph is a year and shows the stacked areas in hectares.

These transitions are done here:

```Javascript
// 3) Target analysis
var classes = {
    0: { src: 3, dst: 15, color: "red" }, // LenC -> Pas
    1: { src: 3, dst: 19, color: "1E90FF" }, // LenC -> CultS
    3: { src: 4, dst: 15, color: "blue"  } // LenA -> Pas
    
}
```
The [legend codes](https://chaco.mapbiomas.org/legend-codes/) can be verified from the [MapBiomas Chaco](https://chaco.mapbiomas.org) website or from other initiatives that wish to be used. They are also provided in the LULC legend.

## Areas corresponding to the forest law regulations (OTBN)

These areas correspond to the total sum of changes in each of the categories of the territorial planning of native forests for all years.

## Layers included in the map

Three layers are included in the map:

1. MapBiomas LULC
2. Target area
3. years of coverage change

# Example: Step-by-Step

## Choose a geometry target

In this case we are going to draw a geometry.

![step-01](images/step-01.png)

## Draw the polygon

![step-02](images/step-02.png)

1. Enable the Drawing tools.
2. Draw the polygon through the location of successive points.
3. Run the analysis and generate the report.


## Reporting

![step-03](images/step-03.png)

1. Administrative limits of provinces and departments where the polygon is located.
2. Total area of the polygon and area of changes.
3. Chart of change surfaces by year.
4. Chart of areas according to OTBN categories.
5. Map of years with changes.
6. Legend showing the years that show changes from forest to agriculture or pasture classes.

In this example, the largest area of change was detected in 2017. There we observed that transition 315 (Closed forest to pasture) was 332 hectares, while transition 319 (Closed forest to agriculture) was 238 hectares for that year.

![step-04](images/step-04.png)










 
