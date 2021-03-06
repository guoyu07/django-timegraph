django-timegraph - monitoring graphs for django  
Copyright (c) 2011-2012, Wifirst  
Copyright (c) 2013, Jeremy Lainé  

[![Build Status](https://travis-ci.org/jlaine/django-timegraph.png)](https://travis-ci.org/jlaine/django-timegraph)

See AUTHORS file for a full list of contributors.

License
=======

django-timegraph is distributed under the BSD license, see the LICENSE
file for details.

Usage
=====

To inject metric values for an arbitrary object 'device':

    from timegraph.models import Metric

    for metric in Metric.objects.all():
        value = request.POST.get(metric.parameter)
        if value:
            metric.set_polling(device, value)

To read back the value for a metric:

    from timegraph.models import Metric

    metric = Metric.objects.get(pk=123)
    metric.get_polling(device)

To plot a graph for the 'device' object:

    from timegraph.views import render_graph

    def graph_device(request, graph_slug, device_mac):
        """
        Renders the given graph for the given device.
        """
        device = get_object_or_404(Device, pk=device_mac)
        graph = get_object_or_404(Graph, slug=graph_slug)
        return render_graph(request, graph, device)

To set the default watermark for the generated graphs:

    import time
    from timegraph.forms import GraphForm

    GraphForm.base_fields['watermark'].initial = '(c) %s My Company' % time.strftime('%Y')

Homepage
========

For more information, please refer to the project homepage:

http://github.com/jlaine/django-timegraph
