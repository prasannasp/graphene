<script type="text/javascript"><?php global $graphene_settings; ?>
	//<![CDATA[
	jQuery(document).ready(function($){
		$('.meta-box-sortables .head-wrap').click(function(){
			$(this).next().toggle();
			return false;
		}).next().hide();
		
		// Toggle all
		$('.toggle-all').click(function(){
			$('.meta-box-sortables .head-wrap').next().toggle();
			return false;
		})
                
		// Show/Hide the slider_type specific options
		$('input[name="graphene_settings\\[slider_type\\]"]').change(function(){
			$('[class*="row_slider_type"]').hide();
			$('.row_slider_type_'+$(this).val()).fadeIn();
		});
		
		// Show/Hide home page panes specific options
		$('input[name="graphene_settings\\[show_post_type\\]"]').change(function(){
			$('[id*="row_show_post_type"]').hide();
			$('#row_show_post_type_'+$(this).val()).fadeIn();
			if ($(this).val()=='cat-latest-posts'){
				$('#row_show_post_type_latest-posts').fadeIn();
			}
		});
		
		// To hide/show complete section
		$('input[data-toggleOptions]').change(function(){
			$(this).closest('table').next().fadeToggle();
		});
		
		// To Show/Hide the widget hooks
		$('a.toggle-widget-hooks').click(function(){
		   $(this).closest('li').find('li.widget-hooks').fadeToggle();
		   return false;
		});
                
		/* Reordering and admin for the social profile links */
		<?php if ( isset( $_GET['page'] ) && $_GET['page'] == 'graphene_options' 
				&& ( !isset( $_GET['tab'] ) || ( isset( $_GET['tab'] ) && $_GET['tab'] == 'general' ) ) ) : ?>
							
			$('#socialprofile-sortable').sortable({ items: '.socialprofile-table', placeholder: 'socialprofile-dragging', opacity: .8 });
			function delete_socialprofile() {
				$(this).closest('table').remove();
				return false;
			}
			$('.socialprofile-del').bind('click', delete_socialprofile);                
			$('#new-socialprofile-type').change(function(){                    
				if ($('#new-socialprofile-type').val() != 'custom') {
					$('#new-socialprofile-iconurl').closest('tr').hide(); // the the custom icon url input
					$('#new-socialprofile-title').val($('#new-socialprofile-type').find("option:selected").text()); // prefill the title for the user                        
				} 
				else {
					$('#new-socialprofile-iconurl').closest('tr').show();
				}
				if ($('#new-socialprofile-type').val() != 'rss') { $('#new-socialprofile-url-description').hide(); } 
				else { $('#new-socialprofile-url-description').show(); }
			});
			$('#new-socialprofile-add').click(function(){
				var $spType = $('#new-socialprofile-type');
				var $spTitle = $('#new-socialprofile-title');
				var $spUrl = $('#new-socialprofile-url');
				var $spIconUrl = $('#new-socialprofile-iconurl');
				if ($spType.val() == '-') { $spType.focus(); }
				else if (!$spTitle.val()) { $spTitle.focus(); }
				else if ($spType.val() != 'rss' && !$spUrl.val()) { $spUrl.focus(); }
				else if ($spType.val() == 'custom' && !$spIconUrl.val()){ $spIconUrl.focus(); }
				else {
					var ix = $('#socialprofile-next-index').val();
					
					var i18n_title = '<?php printf( __('%s link', 'graphene'), '|TITLE|' ); ?>'.replace('|TITLE|', $spTitle.val());
					var rowspan = 2;
					var icon = '<div class="mysocial social-'+$spType.val()+'">&nbsp;</div>'
					var extraCustom = '';
					if ($spType.val() == 'rss'){
						extraCustom = '<br /><span class="description">'+ $('#new-socialprofile-url-description').text() + '</span>';
					}
					else if ($spType.val() == 'custom'){
						rowspan = 3;
						icon = '<img class="mysocial-icon" src="'+$spIconUrl.val()+' " />';
						extraCustom = '\
								</td>\
							</tr>\
							<tr>\
								<th class="small-row"><?php _e('Icon Url', 'graphene'); ?></th>\
								<td><input type="text" name="graphene_settings[social_profiles]['+ix+'][icon_url]" value="'+$spIconUrl.val()+'" class="widefat code" />';
					}
																	 
					$('#socialprofile-sortable').append(
						'<table class="form-table socialprofile-table">\
							<tr>\
								<th scope="row" rowspan="'+rowspan+'" class="small-row">\
									'+i18n_title+'<br />\
									<input type="hidden" name="graphene_settings[social_profiles]['+ix+'][type]" value="'+$spType.val()+'" />\
									'+icon+'\
								</th>\
								<th class="small-row"><?php _e('Title', 'graphene'); ?></th>\
								<td><input type="text" name="graphene_settings[social_profiles]['+ix+'][title]" value="'+$spTitle.val()+'"  class="widefat code"/>\
							</tr>\
							<tr>\
								<th class="small-row"><?php _e('Url', 'graphene'); ?></th>\
								<td>\
									<input type="text" name="graphene_settings[social_profiles]['+ix+'][url]" value="'+$spUrl.val()+'" class="widefat code" />\
									'+extraCustom+'\
									<br /><span class="delete"><a href="#" class="socialprofile-del"><?php _e( 'Delete', 'graphene' ); ?></a></span>\
								</td>\
							</tr>\
						</table>'
					);
					
					// reset the new form
					$('#socialprofile-next-index').val(ix+1);
					$('option:first', $spType).attr('selected', 'selected');
					$spTitle.val('');
					$spUrl.val('');
					$spIconUrl.val('').closest('tr').hide();
					// rebind the del click event
					$('.socialprofile-del').unbind('click');
					$('.socialprofile-del').bind('click', delete_socialprofile);                        
				}
				return false;
			});
		<?php endif; ?>
                               		
		/* jQuery UI Slider for the column widths options */
		<?php if ( strpos( $_SERVER["REQUEST_URI"], 'page=graphene_options&tab=display' ) ) : ?>
		var gutter = 10;
		var grid_width = <?php echo $graphene_settings['grid_width']; ?>;
		var container_width = <?php echo $graphene_settings['container_width']; ?>;
		var container = container_width - gutter * 2;
		var content_2col = <?php echo $graphene_settings['column_width']['two-col']['content']; ?>;
		var sidebar_left_3col = <?php echo $graphene_settings['column_width']['three-col']['sidebar_left']; ?>;
		var sidebar_right_3col = <?php echo $graphene_settings['column_width']['three-col']['sidebar_right']; ?>;
		
		/* Container */
		$( '#container_width-slider' ).slider({
			min: 800,
			max: 1400,
			step: 5,
			value: container_width,
			slide: function( event, ui ) {
				$( '#container_width' ).val( ui.value );
				container_width = ui.value;
				$( '.column_width-max-legend' ).html( ui.value + ' px' );
				grid_width = (ui.value - gutter * 32) / 16;
				$( '#grid_width' ).val( grid_width );
				container = container_width - gutter * 2;
				
				sidebar_2col = grid_width * 5 + gutter * 8;
				sidebar_3col = grid_width * 4 + gutter * 6;
				
				/* Update the two-column width settings */
				$( "#column_width_2col-slider" ).slider( "option", "max", container - gutter );
				$( "#column_width_2col-slider" ).slider( "option", "value", container - sidebar_2col - gutter );
				$( "#column_width_2col_sidebar" ).val( sidebar_2col );
				$( "#column_width_2col_content" ).val( container - sidebar_2col - gutter * 2 );
				
				/* Update the three-column width settings */
				$( "#column_width-slider" ).slider( "option", "max", ui.value - gutter * 2 );
				$( "#column_width-slider" ).slider( "option", "values", [ sidebar_3col, ui.value - sidebar_3col - gutter * 2] );
				$( "#column_width_sidebar_left" ).val( sidebar_3col );
				$( "#column_width_sidebar_right" ).val( sidebar_3col );
				$( "#column_width_content" ).val( grid_width * 8 + gutter * 14 );
			}	
		});
		
		/* Two-column mode */
		$( '#column_width_2col-slider' ).slider({
			min: gutter,
			max: container - gutter,
			value: content_2col + gutter,
			step: 5,
			slide: function( event, ui ) {
				sidebar_2col = container - ui.value - gutter;
				content_2col = ui.value - gutter;
				
				$( "#column_width_2col_sidebar" ).val( sidebar_2col );
				$( "#column_width_2col_content" ).val( content_2col );
			}
		});
		
		/* Three-column mode */
		$( '#column_width-slider' ).slider({
			range: true,
			min: 0,
			max: container,
			values: [ sidebar_left_3col, container - sidebar_right_3col ],
			step: 5,
			slide: function( event, ui ) {
				sidebar_left = ui.values[0];
				sidebar_right = container - ui.values[1];
				content = container - sidebar_left - sidebar_right - gutter * 4;
				
				$( "#column_width_sidebar_left" ).val( sidebar_left );
				$( "#column_width_sidebar_right" ).val( sidebar_right );
				$( "#column_width_content" ).val( content );
			}
		});
		
		<?php endif; ?>
		
		
		/* Farbtastic colour picker */ 
		<?php if ( strpos( $_SERVER["REQUEST_URI"], 'page=graphene_options&tab=display' ) ) : ?>
		<?php for ($i = 1; $i < 28; $i++) : ?>
		$('#colorpicker-<?php echo $i; ?>').hide();
		color_<?php echo $i; ?> = $.farbtastic('#colorpicker-<?php echo $i; ?>', ".color-<?php echo $i; ?>");
		$(".color-<?php echo $i; ?>").focusin(function(){$('#colorpicker-<?php echo $i; ?>').show()});
		$(".color-<?php echo $i; ?>").focusout(function(){$('#colorpicker-<?php echo $i; ?>').hide()});
		<?php endfor; ?>
		$('.clear-color').click(function(){
			$(this).prev().attr('value', '');
			$(this).prev().removeAttr('style');
			return false;
		});
		<?php endif; ?>
		
		// The widget background preview
		$('#colorpicker-8 div, #colorpicker-9 div, #colorpicker-10 div, #colorpicker-11 div, #colorpicker-12 div, .color-8, .color-9, .color-10, .color-11, .color-12').bind('mouseup keyup', function(){
			$('.sidebar-wrap h3').attr('style', '\
				background: ' + color_12.color + ';\
				background: -moz-linear-gradient(' + color_12.color + ', ' + color_11.color + ');\
				background: -webkit-linear-gradient(' + color_12.color + ', ' + color_11.color + ');\
				background: linear-gradient(' + color_12.color + ', ' + color_11.color + ');\
				border-color: ' + color_8.color + ';\
				color: ' + color_9.color + ';\
				text-shadow: 0 -1px 0 ' + color_10.color + ';\
			');
		});
		$('#colorpicker-6 div, .color-6').bind('mouseup keyup', function(){
			$('.sidebar-wrap').attr('style', 'background: ' + color_6.color + ';');
		});
		$('#colorpicker-7 div, .color-7').bind('mouseup keyup', function(){
			$('.sidebar ul li').attr('style', 'border-color: ' + color_7.color + ';');
		});
		
		// The slider background preview
		$('#colorpicker-13 div, #colorpicker-14 div, .color-13, .color-14').bind('mouseup keyup', function(){
			$('#grad-box').attr('style', '\
				background: ' + color_13.color + ';\
				background: linear-gradient(left top, ' + color_13.color + ', ' + color_14.color + ');\
				background: -moz-linear-gradient(left top, ' + color_13.color + ', ' + color_14.color + ');\
				background: -webkit-linear-gradient(left top, ' + color_13.color + ', ' + color_14.color + ');\
			');
		});
		
		// Block button preview
		$('#colorpicker-15 div, #colorpicker-16 div, #colorpicker-17 div, .color-15, .color-16, .color-17').bind('mouseup keyup', function(){
			
			R = hexToR(color_15.color) - 35;
			G = hexToG(color_15.color) - 35;
			B = hexToB(color_15.color) - 35;
			color_bottom = 'rgb(' + R + ', ' + G + ', ' + B + ')';
			
			$('.block-button').attr('style', '\
					background: ' + color_15.color + ';\
					background: -moz-linear-gradient(' + color_15.color + ', ' + color_bottom + ');\
					background: -webkit-linear-gradient(' + color_15.color + ', ' + color_bottom + ');\
					background: linear-gradient(' + color_15.color + ', ' + color_bottom + ');\
					border-color: ' + color_bottom + ';\
					text-shadow: 0 -1px 0 ' + color_17.color + ';\
					color: ' + color_16.color + ';\
			');
		});
		
		// Archive title preview
		$('#colorpicker-18 div, #colorpicker-19 div, .color-18, .color-19').bind('mouseup keyup', function(){
			$('.page-title').attr('style', '\
				background: ' + color_18.color + ';\
				background: linear-gradient(left top, ' + color_18.color + ', ' + color_19.color + ');\
				background: -moz-linear-gradient(left top, ' + color_18.color + ', ' + color_19.color + ');\
				background: -webkit-linear-gradient(left top, ' + color_18.color + ', ' + color_19.color + ');\
			');
		});
		$('#colorpicker-20 div, .color-20').bind('mouseup keyup', function(){
			$('.page-title').css('color', color_20.color);
		});
		$('#colorpicker-21 div, .color-21').bind('mouseup keyup', function(){
			$('.page-title span').css('color', color_21.color);
		});
		$('#colorpicker-22 div, .color-22').bind('mouseup keyup', function(){
			$('.page-title').css('text-shadow', '0 -1px 0 ' + color_22.color);
		});
                
        
		// Non-essential options display settings
		/* Disabled for now, until proper API is implemented for feature pointers in WordPress core
		var nonEssentialOptions = grapheneGetCookie('graphene-neod'); // neod = Non Essential Options Display
		if (nonEssentialOptions == 'true'){
			$('.non-essential-option, .toggle-essential-options, .nav-tab-advanced').show();
			$('.toggle-all-options').hide();
		} else {
			$('.non-essential-option, .toggle-essential-options, .nav-tab-advanced').hide();
			$('.toggle-all-options').show();
		}
		
		$('.toggle-essential-options').click(function(){
			grapheneSetCookie('graphene-neod', false, 100);
			$('.non-essential-option, .toggle-essential-options, .nav-tab-advanced').hide();
			$('.toggle-all-options').show();
			return false;
		});
		$('.toggle-all-options').click(function(){
			grapheneSetCookie('graphene-neod', true, 100);
			$('.non-essential-option, .toggle-essential-options, .nav-tab-advanced').show();
			$('.toggle-all-options').hide();
			return false;
		});
		*/		
		
		
		// Remember the opened options panes
		$('.meta-box-sortables .head-wrap, .toggle-all').click(function(){
			var postboxes = $('.left-wrap .postbox');
			var openboxes = new Array();
			$('.left-wrap .panel-wrap:visible').each(function(index){   
				var openbox = $(this).parent();
				openboxes.push(postboxes.index(openbox));                        
			});                    
			grapheneSetCookie('graphene-tab-<?php echo (isset($_GET['tab'])) ? $_GET['tab'] : 'general'; ?>-boxes', openboxes.join(','), 100);                    
		});
		
		// reopen the previous options panes
		var oldopenboxes = grapheneGetCookie('graphene-tab-<?php echo (isset($_GET['tab'])) ? $_GET['tab'] : 'general'; ?>-boxes');                
		if (oldopenboxes != null && oldopenboxes != '') {
			var boxindexes = oldopenboxes.split(',');                    
			for (var boxindex in boxindexes){                            
				$('.left-wrap .postbox:eq('+boxindexes[boxindex]+')').find('.panel-wrap').show();
			}
		}
		
	});
	
	function hexToR(h) {
		if ( h.length == 4 )
			return parseInt((cutHex(h)).substring(0,1)+(cutHex(h)).substring(0,1),16);
		if ( h.length == 7 )
			return parseInt((cutHex(h)).substring(0,2),16);
	}
	function hexToG(h) {
		if ( h.length == 4 )
			return parseInt((cutHex(h)).substring(1,2)+(cutHex(h)).substring(1,2),16);
		if ( h.length == 7 )
			return parseInt((cutHex(h)).substring(2,4),16);
	}
	function hexToB(h) {
		if ( h.length == 4 )
			return parseInt((cutHex(h)).substring(2,3)+(cutHex(h)).substring(2,3),16);
		if ( h.length == 7 )
			return parseInt((cutHex(h)).substring(4,6),16);
	}
	function cutHex(h) {return (h.charAt(0)=="#") ? h.substring(1,7):h}

	function grapheneSetCookie(name,value,days) {
		if (days) {
			var date = new Date();
			date.setTime(date.getTime()+(days*24*60*60*1000));
			var expires = "; expires="+date.toGMTString();
		}
		else var expires = "";
		document.cookie = name+"="+value+expires+"; path=/";
	}

	function grapheneGetCookie(name) {
		var nameEQ = name + "=";
		var ca = document.cookie.split(';');
		for(var i=0;i < ca.length;i++) {
			var c = ca[i];
			while (c.charAt(0)==' ') c = c.substring(1,c.length);
			if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length,c.length);
		}
		return null;
	}

	function grapheneDeleteCookie(name) {
		grapheneSetCookie(name,"",-1);
	}
	
	// To support the Media Uploader/Gallery picker in the theme options
	jQuery(document).ready(function() {
		var uploadparent = 0;
		var old_send_to_editor = window.send_to_editor;
		var old_tb_remove = window.tb_remove;
		
		jQuery('.upload_image_button').click(function(){
			uploadparent = jQuery(this).closest('td');
			tb_show('', 'media-upload.php?post_id=0&amp;type=image&amp;TB_iframe=true');
			return false;
		});
		
		window.tb_remove = function() {
			uploadparent = 0;
			old_tb_remove();
		}
		
		window.send_to_editor = function(html) {
			if(uploadparent){              
				imgurl = jQuery('img',html).attr('src');
				uploadparent.find('input[type="text"]').attr('value', imgurl);
				tb_remove();
			} else {
				old_send_to_editor();
			}
		}
	});
//]]>
</script>