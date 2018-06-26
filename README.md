# kamon-graphite

Write report metrics in graphite format.
Per default the graphite tag support (available since graphite 1.1) is enabled (see include-tags feature flag).

## Config
    kamon{
        graphite {
            # Hostname and port in which your Carbon daemon is running.
            hostname = "127.0.0.1"
            port = 2003
    
            # Prefix for all metrics sent to Graphite.
            metric-name-prefix = "kamon-graphite"
    
            # include tags as suffix to metric name (format graphite 1.1) metricname;tag1=value1;tag2=value2
            # without this enabled you might get multiple values for the same metric! - but may be necessary for legacy applications
            include-tags = true
    
            additional-tags {
                service = "yes"
                host = "yes"
                instance = "yes"
                blacklisted-tags = []
            }
    
            filter-config-key = "graphite-tag-filter"
    
        }
        util.filters {
            graphite-tag-filter {
                includes = ["**"]
                excludes = []
            }
        }
    }

## Failure handling
When sending metrics at a tick interval fails the current snapshot will be dropped and the next snapshot will try to send metrics using new connection.
    
   
## Possible enhancements
* configure percentiles - currently hardcoded to 50,90,99
* configure additional tags to be sent
* configure tag filters