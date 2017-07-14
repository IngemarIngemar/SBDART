# SBDART
SBDART (Santa Barbara DISORT Atmospheric Radiative Transfer) is a FORTRAN computer code designed for the analysis of a wide variety of plane-parallel radiative transfer problems encountered in satellite remote sensing and atmospheric energy budget studies. The program is based on a collection of highly developed and reliable physical models, which have been developed by the atmospheric science community over the past few decades. The following discussion is a brief introduction to the key components of the code and the models on which they are based.

Cloud Model

Clouds are a major modulator of the earths climate, both by reflecting visible radiation back out to space and by intercepting part of the infrared radiation emitted by the Earth and re-radiating it back to the surface. The computation of radiative transfer within a cloudy atmosphere requires knowledge of the scattering efficiency, the single scattering albedo, which is the probability that a extinction event scatters rather than absorbs a photon, and the asymmetry factor, which indicates the strength of forward scattering. SBDART contains an internal database of these parameters for clouds composed of spherical water or ice droplets. This internal database was computed with a Mie scattering code and covers a range of particle size effective radius in the range 2 to 128um. (The effective radius is the ratio of the third and second moments of the droplet radius distribution). By default, the angular distribution of scattered photons is based on the simple Henyey- Greenstein parameterization, but more detailed scattering functions may be input as desired. (The Henyey- Greenstein approximation has been shown to provide good accuracy when applied to radiative flux calculations (van de Hulst, 1968; Hansen, 1969).

Gas Absorption Model

In its standard mode of operation SBDART relies on low resolution band models developed for the LOWTRAN 7 atmospheric transmission code (Pierluissi and Marogoudakis, 1986). These models provide the clear sky atmospheric transmisson from 0 to 50000 cm-1 and include the effects of all radiatively active molecular species found in the earth's atmosphere. The models were derived from detailed line-by-line calculations which were degraded to 20 cm-1 resolution for use in LOWTRAN. This translates to a wavelength resolution of about 5 nm in the visible and about 200 nm in the thermal infrared.
                       1
Because these band models represent rather large wavelength bins, the transmission functions do
not necessarily follow Beers law; i.e., the fractional transmission through a slab of material depends not only on the slab thickness but also on the amount of material penetrated before entering the slab. In order to allow these transmission functions to be used with DISORT (which assumes Beers law behavior), the band models are approximated with a three term exponential fit (Wiscomb and
Evans, 1977).

A capability to read high resolution k-distribution optical depths from a disk file was introduced in SBDART version 2.0. This mode of operation is less convenient to use than the standard approach, as it requires use of another program, which accesses a large spectral database to generate the high resolution files. However, it has the advantage of removing limitations in the ultimate spectral resolution available with SBDART. The ancillary programs, CKLW and CKSW, may be used to create these high-spectral resolution optical depth files. These programs have not been exercised as thoroughly as SBDART. For now, they should be considered experimental.

Extraterrestrial Source Spectra

To facilitate comparison with other radiative transfer codes, SBDART may be run with any of three extraterrestrial solar spectrum models. The default is to use the LOWTRAN-7 solar spectrum (Thekeakara, 1974). This model is based on measurements between 300 and 610nm and uses a lambda-4 power law for longer wavelengths. Optionally, SBDART may be run with the solar models used in 5s (Tanre et al. 1990) or MODTRAN-3. The MODTRAN-3 model is probably the most accurate. It is a composite of information gathered by several different spectral measurement campaigns. For wavelengths between 174 and 351nm the spectral information is based on observations made with the Solar Ultraviolet Spectral Irradiance Monitor flown on Spacelab 2 (VanHoosier et al. 1988). Wavelengths between 351 and 868nm are based on the results of Neckel and Labs (1984). The observations of Wehrli (1985) are used for wavelengths between 0.868 and 3.226um. And finally, for wavelengths greater 3.23um, the longwave power law dependence of LOWTRAN-7 (Thekeakara, 1974) is used.

Standard Atmospheric Models

We have adopted six standard atmospheric profiles from the 5s atmospheric radiation code which are intended to model the following typical climatic conditions: tropical, midlatitude summer, midlatitude winter, subarctic summer, subarctic winter and US62. These model atmospheres (McClatchey et al, 1971) have been widely used in the atmospheric research community and provide standard vertical profiles of pressure, temperature, water vapor and ozone density. In addition, the user can specify their own model atmosphere based on, for example, a series of radiosonde profiles. The concentration of trace gases such as CO2 or CH4 are assumed to make up a fixed fraction (which may be specified by the user) of the total particle density.

Standard Aerosol Models

SBDART can compute the radiative effects of several common boundary layer and upper atmosphere aerosol types. In the boundary layer, the user can select either rural, urban, or maritime aerosols. These models differ from one another in the way their scattering efficiency, single scattering albedo and asymmetry factors vary with wavelength. The total vertical optical depth of boundary layer aerosols is derived from user specified horizontal meteorologic visibility at 0.55 um and an internal vertical distribution model. In the upper atmosphere up to 5 aerosol layers can be specified, with radiative characteristics that model fresh and aged volcanic, meteoric and the climitologic tropospheric background aerosols. The aerosol models included in SBDART were derived from those provided in the 5s (Tanre, 1988) and LOWTRAN7 computer codes (Shettle and Fenn, 1975).

Radiative Transfer Equation Solver

The radiative transfer equation is numerically integrated with DISORT (DIScreet Ordinate Radiative Transfer, Stamnes et al, 1988). The discrete ordinate method provides a numerically stable algorithm to solve the equations of plane-parallel radiative transfer in a vertically inhomogeneous atmosphere. The intensity of both scattered and thermally emitted radiation can be computed at different heights and directions. SBDART is configured to allow up to 65 atmospheric layers and 40 radiation streams (40 zenith angles and 40 azimuthal modes).

Surface Models

The ground surface cover is an important determinant of the overall radiation environment. In SBDART six basic surface types -- ocean water (Viollier, 1980), lake water (Kondratyev, 1969), vegetation (Manual of Remote Sensing), snow (Wiscombe and Warren, 1980) and sand (Staetter and Schroeder, 1978) -- are used to parameterize the spectral reflectivity of the surface. The spectral reflectivity of a large variety of surface conditions is well approximated by combinations of these basic types. For example, the fractions of vegetation, water and sand can be adjusted to generate a new spectral reflectivity representing new/old growth, or deciduous vs evergreen forest. Combining a small fraction of the spectral reflectivity of water with that of sand yields an overall spectral dependence close to wet soil.
