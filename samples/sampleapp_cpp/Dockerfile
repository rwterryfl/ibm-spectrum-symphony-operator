# 
# BuildConfig Docker strategy for Symphony SmapleApp C++ example
#

FROM registry.connect.redhat.com/ibm/spectrum-symphony@sha256:1722eae3debcab3354a17c019cb38dc15acb71c6fed33585f669c9caceefc877 AS build-env
USER root

RUN microdnf install --nodocs gcc-c++ 

COPY ./src/ /opt/app/

RUN \
       . /opt/ibm/spectrumcomputing/profile.platform \
    && make -C /opt/app all

FROM registry.connect.redhat.com/ibm/spectrum-symphony@sha256:1722eae3debcab3354a17c019cb38dc15acb71c6fed33585f669c9caceefc877 AS run-env
USER root

COPY --from=build-env /opt/app/Output/ /opt/app/

RUN chown -R 1000:0 /opt/app && chmod -R g=u /opt/app

USER 1000

ENTRYPOINT ["/opt/app/run"]
