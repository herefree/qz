**flink源码个人理解**

一、生成StreamGraph模块

http://matt33.com/2019/12/08/flink-stream-graph-2/

StreamGraph 内存储着StreamNode的Map，由StreamNode内部存储Streamedage

addStreamNode 然后addStreamedge的时候会得到StreamNode并在其中加入Streamedge，也就是说StreamNode里面存储着StreamEdge。
二、生成JObGraph
从后向前先把后面的可以Chain在一块的算子，Chain在一块然后生成JobVetix，然后在生成前面的JobVetix，然后通过connect生成DateSet与JobEdge连接起来。transitiveOutEdges来记录两个JobVetix之间的Edge。
if (currentNodeId.equals(startNodeId)) {

				config.setChainStart();
				config.setChainIndex(0);
				config.setOperatorName(streamGraph.getStreamNode(currentNodeId).getOperatorName());
				config.setOutEdgesInOrder(transitiveOutEdges);
				config.setOutEdges(streamGraph.getStreamNode(currentNodeId).getOutEdges());

				for (StreamEdge edge : transitiveOutEdges) {
					connect(startNodeId, edge);
				}
        //是startNode会把configs添加到config
				config.setTransitiveChainedTaskConfigs(chainedConfigs.get(startNodeId));

			} else {
				chainedConfigs.computeIfAbsent(startNodeId, k -> new HashMap<Integer, StreamConfig>());

				config.setChainIndex(chainIndex);
				StreamNode node = streamGraph.getStreamNode(currentNodeId);
				config.setOperatorName(node.getOperatorName());
        //不是startNode会把config添加到chainedConfigs
				chainedConfigs.get(startNodeId).put(currentNodeId, config);
			}
