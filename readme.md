# WaveformDT

Python implementation of LabVIEW's waveform data type

LabVIEW's waveform data type has three required attributes: t0, dt, and Y.
Additional attributes can be set and are included in the returned WaveformDT.
WaveformDT has the function to_xy() that will generate the x-axis array from the
t0, dt and number of samples in the Y array.

Attributes:
    Y (array-like): data
    dt (float): wf_increment
    t0 (float or datetime): wf_start_time

Example:

    >>> data = WaveformDT([1,2,3], 1, 0)
    >>> x, y = data.to_xy()
    >>> x
    array([0., 1., 2.])
    >>> y
    array([1, 2, 3])

WaveformDT supports a variety of workflows with and without units where unit
support is provided by the Unyt library.

    >>> data.xunit = "s"
    >>> data.yunit = "V"
    >>> x, y = data.to_xy()
    >>> x
    unyt_array([0., 1., 2.], 's')
    >>> y
    unyt_array([0, 1, 2], 'V')

WaveformDT supports Matplotlib and its labeled data interface:

    >>> import matplotlib.pyplot as plt
    >>> waveform = WaveformDT([1,2,3], 1, 0)
    >>> plt.plot('x', 'y', 'r-', data=waveform)
    [<matplotlib.lines.Line2D object ... >]
    >>> plt.show()

Note:
    The x-axis array will be relative time by default. For absolute time, set the
    relative parameter to False.