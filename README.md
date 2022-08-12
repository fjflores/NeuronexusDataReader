# NeuronexusDataReader
Set of matlab files to read xdat files produced by the neuronexus recording setup.

## Example Usage
With current folder set to ~/radix/data, list available files
```matlab
dir
```
```
. 
..
import_test_xdat__uid1003-10-43-13.xdat.json      
import_test_xdat__uid1003-10-43-13_data.xdat      
import_test_xdat__uid1003-10-43-13_timestamp.xdat 
```

Create the reader
```matlab
reader = allegoXDatFileReader
```
```
reader = 

  struct with fields:

      getAllegoXDatAllSigs: @getAllegoXDatAllSigs
      getAllegoXDatPriSigs: @getAllegoXDatPriSigs
      getAllegoXDatAuxSigs: @getAllegoXDatAuxSigs
      getAllegoXDatDinSigs: @getAllegoXDatDinSigs
     getAllegoXDatDoutSigs: @getAllegoXDatDoutSigs
    getAllegoXDatTimeRange: @getAllegoXDatTimeRange
```

Choose the file to import. Just use the base name, not the extension or the '_data' or '_timestamp' portions

```matlab
datasource = 'import_test_xdat__uid1003-10-43-13'
```

```
datasource =

    'import_test_xdat__uid1003-10-43-13'
```

View the time range of the file

```matlab
reader.getAllegoXDatTimeRange(datasource)
```

```
ans =

    1.9565    7.1424
```

Import all the signals with timestamps from 2 through 6 seconds

```matlab
signalStruct = reader.getAllegoXDatAllSigs(datasource, [2 6])
```

```
signalStruct = 

  struct with fields:

        signals: [134×120000 single]
     timeStamps: [1×120000 int64]
    timeSamples: [1×120000 double]
```

Plot a subset of the data

```matlab
plot( signalStruct.timeSamples( 1 : 100 ), signalStruct.signals( 1 : 10, 1 : 100 ) )
```

Import all the signals with all the timestamps

```matlab
signalStruct = reader.getAllegoXDatAllSigs( datasource, [ -1 -1 ] );
```
